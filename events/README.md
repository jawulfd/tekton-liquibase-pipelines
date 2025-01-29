# Tekton Events Configuration

This folder contains the tekton events and triggers configurations which are required to call [liquibase-pipeline](../pipelines/liquibase-pipeline.yaml)
when there is a change in GitHub

### Tekton Event Listener

You can find sample yaml files for different configurations of EventListeners:

- [eventlistener-simple.yaml](eventlistener-simple.yaml) only listen to push events which come from GitHub
- [eventlistener-multi.yaml](eventlistener-multi.yaml) listen to push events to develop branch and merged Pull Requests to main or master branch
- [eventlistener-multi-tag.yaml](eventlistener-multi-tag.yaml) list to merged Pull Requests to develop branch and creation of tags

Inside the EventListener, you can reference different triggers configuration and each trigger can point to different TriggerBindings and TriggerTemplates

This EventListener creates a service with the name el-<event-listener-name> which can be used to create a public endpoint to configure GitHub webhooks

### Tekton Trigger Template

A TriggerTemplate is a resource that specifies a blueprint for the resource, such as a TaskRun or PipelineRun, 
that you want to instantiate and/or execute when your EventListener detects an event. 
It exposes parameters that you can use anywhere within your resource’s template.

[trigger-template.yaml](trigger-template.yaml) has the configuration to trigger a PipelineRun for [liquibase-pipeline](../pipelines/liquibase-pipeline.yaml)
when an event is detected

### Tekton Trigger Binding

A TriggerBinding allows you to extract fields from an event payload and bind them to named parameters that can then be used in a TriggerTemplate.
As Tekton uses named parameters, the parameters names which are used in TriggerBindings must match the corresponding ones in TriggerTemplate  

In [trigger-binding.yaml](trigger-binding.yaml) the TriggerBindings for branch and tag event types can be found, along with
TriggerBindings samples for environment configuration
