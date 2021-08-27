# Implement a BPMN Exclusive Gatewayin Camunda
The article contains a step-by-step guide on how to implement a BPMN Exclusive Gateway in Camunda making use of a Spring Boot Application. A diverging Exclusive Gateway (Decision) is used to create alternative paths within a Process flow. This is basically the “diversion point in the road” for a Process. For a given instance of the Process, only one of the paths can be taken. A converging Exclusive Gateway is used to merge alternative paths. Each incoming Sequence Flow token is routed to the outgoing Sequence Flow without synchronization.

**Java Nibble Article:** [https://www.javanibble.com/implement-bpmn-exclusive-gateway-in-camunda/](https://www.javanibble.com/implement-bpmn-exclusive-gateway-in-camunda/)

## Pre-Requisites
The following is required to run the Spring Boot example:
* [curl](https://www.javanibble.com/how-to-install-curl-on-macos-using-homebrew/)
* jq
* [maven](https://www.javanibble.com/how-to-install-maven-on-macos-using-homebrew/)

## BPMN Exclusive Gateway
> An exclusive gateway, is used to model a decision in the process. When the execution arrives at this gateway, all outgoing sequence flows are evaluated in the order in which they have been defined. The sequence flow which condition evaluates to ‘true’ is selected for continuing the process.

Use Camunda Modeller to model the process. The process model is composed of five tasks and two exclusive gateways:

![BPMN Exclusive Gateway](https://www.javanibble.com/assets/images/posts/bpmn-exclusive-gateway/bpmn-exclusive-gateway.png)

* Retrieve Coffee Order: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Choice of Coffee: Is a `Exclusive Gateway` with three sequence flows.
* Espresso: Is a `Sequence Flow` with an expression `#{order == 'Espresso'}`.
* Caffè Mocha: Is a `Sequence Flow` with an expression `#{order == 'Caffe Mocha'}`.
* Default: Is the default `Sequence Flow`.
* Make Espresso: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Make Caffè Mocha: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Give Free Sample: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Deliver Coffee Order:Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.

