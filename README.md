# Ambassador

Ambassador provides a way to communicate between node.js processes.

## Installation

	npm install ambassador --save
	
## Usage

Process A (pid: 14100)

```js
// listen to signal 'watch'
require('ambassador').on('watch', function(pid, data){
	console.log('Signal "watch" from process[', pid, '] with data', data);
});
```

Process B (pid: 14102)

```js
// send data to process 14100 (A)
require('ambassador').send(14100, 'watch', {
	abc: 1
});
```

Then, process A will print:

	Signal "watch" from process[ 14102 ] with data {abc: 1}
	

### ambassador.send(pid, type, data);

Send a `type` signal to the process `pid` with data `data`

##### Returns `ambassador`

##### pid `Number`

The pid of the target process

##### type `String`

Signal type

##### data `mixed`

The data to be sent


### ambassador.on(type, callback)

##### type `String`

##### callback `function(pid, data)`

The callback function

##### pid `Number`

The pid number from which process the signal has been sent.

##### data `mixed`

The received data
 