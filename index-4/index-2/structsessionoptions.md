# class tensorflow::SessionOptions

Configuration information for a Session .

## Member Details

### `Env* tensorflow::SessionOptions::env` <a id="Env_tensorflow_SessionOptions_env"></a>

The environment to use.

### `string tensorflow::SessionOptions::target` <a id="string_tensorflow_SessionOptions_target"></a>

The TensorFlow runtime to connect to.

If 'target' is empty or unspecified, the local TensorFlow runtime implementation will be used. Otherwise, the TensorFlow engine defined by 'target' will be used to perform all computations.

"target" can be either a single entry or a comma separated list of entries. Each entry is a resolvable address of the following format: local ip:port host:port ... other system-specific formats to identify tasks and jobs ...

NOTE: at the moment 'local' maps to an in-process service-based runtime.

Upon creation, a single session affines itself to one of the remote processes, with possible load balancing choices when the "target" resolves to a list of possible processes.

If the session disconnects from the remote process during its lifetime, session calls may fail immediately.

### `ConfigProto tensorflow::SessionOptions::config` <a id="ConfigProto_tensorflow_SessionOptions_config"></a>

Configuration options.

### `tensorflow::SessionOptions::SessionOptions()` <a id="tensorflow_SessionOptions_SessionOptions"></a>

