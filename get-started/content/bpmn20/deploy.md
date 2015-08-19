---

title: 'Deploy and Test the BPMN 2.0 Process'
weight: 40

menu:
  main:
    name: "Deploy and Test"
    parent: "get-started-pa"
    identifier: "get-started-pa-deploy"
    pre: "Build and deploy the web application to Apache Tomcat. Test the BPMN 2.0 Process with Tasklist and Cockpit." 
    
---

The next step consists in building, deploying and testing the process.

# Build the Web Application with Maven

Select the `pom.xml` in the Package Explorer, perform a right-click and select `Run As / Maven Install`. This will generate a WAR file named `loan-approval-0.0.1-SNAPSHOT.war` In the `target/` folder of your Maven project.

{{< note title="Hint" class="info" >}}
If the `loan-approval-0.0.1-SNAPSHOT.war` file is not visible after having performed the Maven build, you need to refresh the project (F5) in eclipse.
{{< /note >}}

# Deploy to Apache Tomcat

In order to deploy the process application, copy-paste the `loan-approval-0.0.1-SNAPSHOT.war` from your Maven project to the `$CAMUNDA_HOME/server/apache-tomcat/webapps` folder.

Check the log file of the Apache Tomcat server. If you see the following log message, the deployment was successful:

<pre class="console">
org.camunda.bpm.application.impl.ServletProcessApplicationDeployer onStartup
INFORMATION: Detected @ProcessApplication class org.camunda.bpm.getstarted.loanapproval.LoanApprovalApplication
org.camunda.bpm.container.impl.deployment.ParseProcessesXmlStep parseProcessesXmlFiles
INFORMATION: Found process application file at .../webapps/loan-approval-0.1.0-SNAPSHOT/WEB-INF/classes/META-INF/processes.xml
org.camunda.bpm.container.impl.deployment.DeployProcessArchiveStep logDeploymentSummary
INFORMATION: Deployment summary for process archive 'loan-approval':

        loan-approval.bpmn

org.camunda.bpm.engine.impl.application.ProcessApplicationManager logRegistration
INFORMATION: ProcessApplication 'Loan Approval App' registered for DB deployments [4ab4d156-7543-11e4-86ad-28d2448a9975]. Will execute process definitions

        approve-loan[version: 1, id: approve-loan:1:4abf58a8-7543-11e4-86ad-28d2448a9975]
Deployment does not provide any case definitions.
org.camunda.bpm.container.impl.RuntimeContainerDelegateImpl deployProcessApplication
INFORMATION: Process Application Loan Approval App successfully deployed.
</pre>

# Verify the deployment with Cockpit

Now use Cockpit to check if the process is successfully deployed. Go to <a href="http://localhost:8080/camunda/app/cockpit" target="_blank">http://localhost:8080/camunda/app/cockpit</a>. Log in with demo / demo. Your process *Loan Approval* is visible on the start screen.

{{< img src="../img/cockpit-loan-approval.png" >}}

# Start a process instance

Next, go to camunda Tasklist (<a href="http://localhost:8080/camunda/app/tasklist" target="_blank">http://localhost:8080/camunda/app/tasklist</a>). Click on the <button class="btn btn-default btn-xs"><i class="glyphicon glyphicon-list-alt"></i> Start process</button> button to start a process instance. This opens a dialog where you can select *Loan Approval* from the list. Now you can set variables for the process instance using a generic form.

{{< img src="../img/start-form-generic.png" >}}

The generic form can be used whenever you have not added a dedicated form for a User Task or a Start Event.
Click on the <button class="btn btn-default btn-xs">Add a variable</button> button to get a new row. Fill in the form as shown in the screenshot. When you are done, click <button class="btn btn-default btn-xs">Start</button>.

If you now go back to <a href="http://localhost:8080/camunda/app/cockpit" target="_blank">camunda Cockpit</a>, you see the newly created process instance that is waiting in the User Task.

# Configure Process Start Authorizations

To allow the user *john* to see the process definition *Loan Approval* you have to go to camunda Admin (<a href="http://localhost:8080/camunda/app/admin/default/#/authorization?resource=6" target="_blank">http://localhost:8080/camunda/app/admin/default/#/authorization?resource=6</a>). Next, click on the button <button class="btn btn-default btn-xs">Create New</button> to add a new authorization on the resource *process definition*. Now you can give the user *john* all permissions on process definition *approve-loan*. When you are done, submit the new authorization.

{{< img src="../img/create-process-definition-authorization.png" >}}

For further details about authorizations and how to manage them please read the following sections in the user guide: <a href="ref:/guides/user-guide/#process-engine-authorization-service" target="_blank">Authorization Service</a> and <a href="ref:/guides/user-guide/#admin-authorization-management-authorizations" target="_blank">Authorizations</a>

# Work on the task

Log out of the Admin. Go to Tasklist (<a href="http://localhost:8080/camunda/app/tasklist" target="_blank">http://localhost:8080/camunda/app/tasklist</a>) and log back in with the user credentials "john / john". Now you see the *Approve Loan* task in your Tasklist. Select the task and click on the `Diagram` tab. This displays the process diagram highlighting the User Task that is waiting for you to work on it.

{{< img src="../img/diagram.png" >}}

To work on the task, select the `Form` tab. Again, there is no task form associated with the process. Click on <button class="btn btn-default btn-xs">Load Variables</button>. This displays the variables you have put in in the first step.

{{< img src="../img/task-form-generic.png" >}}