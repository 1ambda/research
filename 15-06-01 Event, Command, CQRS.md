# Event vs Command

http://programmers.stackexchange.com/questions/228807/how-to-determine-if-a-message-should-be-a-command-message-or-event-message

`ShipOrder` is a command and the sender will likely to expect a response of some sort.

`OrderShipped` is a declaration and the sender is unlikely to expect a response.

An **Event** message is something that has just happened. You are notifying of the event that has just happened.

A **Command** message is a message that expects something to be done. It may or mat nor expect a response.

> Favoring events over commands results in less coupling. The emitter of the event does not care about the consumer. In a command pattern the caller knows and it therefore dependent on the existence of the provider.

# Intro to Akka persistence

https://www.youtube.com/watch?v=r5lecCBazvE

slide : http://www.slideshare.net/patriknw/akka-persistence-webinar

# CQRS

![](http://pds24.egloos.com/pds/201110/08/63/c0043363_4e900731e107b.png)

https://www.youtube.com/watch?v=JHGkaShoyNs

> State transition are an important part of our problem space and should be modeled with in our domain
