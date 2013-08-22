# Ambassador

Ambassador provides a way to communicate between node.js processes.

## Installation

	npm install ambassador --save
	
## Usage

First of all, `ambassador` is an [`EventEmitter`](http://nodejs.org/api/events.html#events_class_events_eventemitter).

### Example

Process A (pid: 14100)

```js
// Listen to signal 'watch'
require('ambassador').on('watch', function(pid, data){
	console.log('Signal "watch" from process[', pid, '] with data', data);
});

// So that process A will hang on.
require('http').createServer(function(){}).listen(9876);
```

Process B (pid: 14102)

```js
// Send data to process 14100 (A)
require('ambassador').send(14100, 'watch', {
	abc: 1
});
```

Then, process A will print:

	Signal "watch" from process[ 14102 ] with data {abc: 1}
	

## Methods

### ambassador.send(pid, signal, data);

Send a `signal` signal to the process `pid` with data `data`

##### Returns `ambassador`

##### pid `Number`

The pid of the target process

##### signal `String`

Signal name

##### data `mixed`

The data to be sent


### ambassador.on(signal, callback)

##### Returns `ambassador`

##### signal `String`

##### callback `function(pid, data)`

The callback function

##### pid `Number`

The pid number from which process the signal has been sent.

##### data `mixed`

The received data


### ambassador.kill(pid)

If the target process contains `ambassador`, this method will safely kill that process.
 