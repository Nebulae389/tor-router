# RPC Functions

The following functions are available via the RPC

## queryInstances()

Returns an array containing information on the instances currently running under the router.

## queryInstanceByName(String)

Returns information on an instance identified by name

## queryInstanceAt(Integer)

Returns information on an instance identified by index

## createInstances(Array or Integer)

If passed an Integer, creates thats many Tor instances. An array can also be passed describing the names, weights and configurations of prospective instances. :

```
var rpcRequest = {
	"method": "createInstances",
	"params": [
		{
			"Config": {

			},
			"Name": "instance-1",
			"Weight": 10
		},
		...
	], 
	"jsonrpc":"2.0", 
	"id": 1
};
```

Will wait until the Tor Instance has fully connected to the network before returning

## addInstances(Array)

Serves the same purpose as "createInstances" but only takes an Array

## removeInstances(Integer)

Removes a number of instances

## removeInstanceAt(Integer)

Remove a specific instance from the pool by its index

## removeInstanceByName(String)

Remove a specific instance from the pool by its name

## newIdentites()

Get new identites for all instances

## newIdentityAt(Integer)

Get a new identity for a specific instance by its index

## newIdentityByName(String)

Get a new identity for a specific instance by its name

## nextInstance()

Cycle to the next instance using the load balancing method

## closeInstances()

Shutdown all Tor instances

## setTorConfig(Object)

Applies the configuration to all active instances

## getDefaultTorConfig() 

Retrieve the default Tor Config for all future instances

## setDefaultTorConfig(Object)

Set the default Tor Config for all future instances

## getLoadBalanceMethod()

Get the current load balance method

## setLoadBalanceMethod(String)

Set the current load balance method

## getInstanceConfigAt(Integer: index, String: keyword)

Retrieves the current value of an option set in the configuration by the index of the instance using the control protocol. 

Example:

The following would retrieve the path to the data directory of the instance

```
var rpcRequest = {
	"method": "getInstanceConfigAt",
	"params": [0, "DataDirectory"], 
	"jsonrpc":"2.0", 
	"id": 1
};
```

## getInstanceConfigByName(String: name, String: keyword)

Works the same way as `getInstanceConfigAt` except takes an instance name instead of an index

## setInstanceConfigAt(Integer: index, String: keyword, String: value)

Sets the value in the configuration of an instance using the control protocol. Changes will be applied immediately.

## setInstanceConfigByName(Integer: index, String: keyword, String: value)

Works the same way as `setInstanceConfigAt` except takes an instance name instead of an index

## signalAllInstances(String)

Sends a signal using the control protocol to all instances

A list of all signals can be [found here](https://gitweb.torproject.org/torspec.git/tree/control-spec.txt)

## signalInstanceAt(Integer: index, String: signal)

Sends a signal using the control protocol to an instance identified by its index

## signalInstanceByName(String: name, String: signal)

Sends a signal using the control protocol to an instance identified by its name