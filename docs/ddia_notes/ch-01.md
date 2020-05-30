# Chapter 01

## Reliability

Fault and failure are not the same.

- Fault: is usually defined as one component of the system deviating from its spec.
- Failure: is when the system as a whole stops providing the required service to the user.

There are different type of faults

- Hardware fault
- Software errors
- Human errors

## Scalability

The ability to cope up with increased load.

### Describe Load

Determine the load parameter(s) that best describe your system.
Eg: *The distribution of followers per user (maybe weighted by how often those users tweet) is a key load parameter for discussing scalability, since it determines the fan-out load*

### Describe Performance

- When you increase a load parameter and keep the system resources (CPU, memory, network bandwidth, etc.) unchanged, how is the performance of your system affected?
- When you increase a load parameter, how much do you need to increase the resources if you want to keep performance unchanged?
- Latency Time: is the duration that a request is waiting to be handled.
- Service Time: is the time taken to process the request
- Response Time: is the time seen by the client. ( includes but not limited to service time, network and queueing delays)

## Maintainability

### Operability

- Runbook 
- Useful scripts

### Simplicity

- Documentation
- Accidental complexity: *a complexity that is not inherent to the problem statement that the application is solving, but arises only from the implementation.*
- Abstraction is one of the best tool to remove *accidental complexity*

### Evolvability

- Agile methodology
- Test Driven Developement (TDD)
  
## Must Reads

- [Chaos Monkey](https://netflixtechblog.com/the-netflix-simian-army-16e57fbab116)
