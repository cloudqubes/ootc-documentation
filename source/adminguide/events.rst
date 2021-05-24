.. 
   "Option One Technologies Cloud" (OOTC) documentation.
   

Event Notification
==================

An event is essentially a significant or meaningful change in the state
of both virtual resources associated with a cloud
environment. Events are used by monitoring systems, usage and billing
systems, or any other event-driven workflow systems to discern a pattern
and make the right business decision. In OOTC an event could be a
state change of virtual  resources, an action performed by an
user (action events), or policy based events (alerts).


Event Logs
----------

There are two types of events in the OOTC Event Log.
Standard events log the success or failure of an event and can be used
to identify jobs or processes that have failed. There are also long
running job events. Events for asynchronous jobs log when a job is
scheduled, when it starts, and when it completes. Other long running
synchronous jobs log when a job starts, and when it completes. Long
running synchronous and asynchronous event logs can be used to gain more
information on the status of a pending job or can be used to identify a
job that is hanging or has not started. The following sections provide
more information on these events..


Notification
------------

Event notification framework provides a means for the Management Server
components to publish and subscribe to OOTC events. Event
notification is achieved by implementing the concept of event bus
abstraction in the Management Server.

A new event for state change, resource state change, is introduced as
part of Event notification framework. Every resource, such as user VM,
volume, NIC, network, public IP, snapshot, and template, is associated
with a state machine and generates events as part of the state change.
That implies that a change in the state of a resource results in a state
change event, and the event is published in the corresponding state
machine on the event bus. All the OOTC events (alerts, action
events, usage events) and the additional category of resource state
change events, are published on to the events bus.


Standard Events
---------------

The events log records three types of standard events.

-  INFO. This event is generated when an operation has been successfully
   performed.

-  WARN. This event is generated in the following circumstances.

   -  When a network is disconnected while monitoring a template
      download.

   -  When a template download is abandoned.

   -  When an issue on the storage server causes the volumes to fail
      over to the mirror storage server.

-  ERROR. This event is generated when an operation has not been
   successfully performed


Long Running Job Events
-----------------------

The events log records three types of standard events.

-  INFO. This event is generated when an operation has been successfully
   performed.

-  WARN. This event is generated in the following circumstances.

   -  When a network is disconnected while monitoring a template
      download.

   -  When a template download is abandoned.

   -  When an issue on the storage server causes the volumes to fail
      over to the mirror storage server.

-  ERROR. This event is generated when an operation has not been
   successfully performed


Event Log Queries
-----------------

Database logs can be queried from the user interface. The list of events
captured by the system includes:

-  Virtual machine creation, deletion, and on-going management
   operations

-  Virtual router creation, deletion, and on-going management operations

-  Template creation and deletion

-  Network/load balancer rules creation and deletion

-  Storage volume creation and deletion

-  User login and logout
