# class tensorflow::Status

## Member Details

### `tensorflow::Status::Status()` <a id="tensorflow_Status_Status"></a>

Create a success status.

### `tensorflow::Status::~Status()` <a id="tensorflow_Status_Status"></a>

### `tensorflow::Status::Status(tensorflow::error::Code code, tensorflow::StringPiece msg)` <a id="tensorflow_Status_Status"></a>

Create a status with the specified error code and msg as a human-readable string containing more detailed information.

### `tensorflow::Status::Status(const Status &s)` <a id="tensorflow_Status_Status"></a>

Copy the specified status.

### `void tensorflow::Status::operator=(const Status &s)` <a id="void_tensorflow_Status_operator_"></a>

### `bool tensorflow::Status::ok() const` <a id="bool_tensorflow_Status_ok"></a>

Returns true iff the status indicates success.

### `tensorflow::error::Code tensorflow::Status::code() const` <a id="tensorflow_error_Code_tensorflow_Status_code"></a>

### `const string& tensorflow::Status::error_message() const` <a id="const_string_tensorflow_Status_error_message"></a>

### `bool tensorflow::Status::operator==(const Status &x) const` <a id="bool_tensorflow_Status_operator_"></a>

### `bool tensorflow::Status::operator!=(const Status &x) const` <a id="bool_tensorflow_Status_operator_"></a>

### `void tensorflow::Status::Update(const Status &new_status)` <a id="void_tensorflow_Status_Update"></a>

If `ok()`, stores `new_status` into `*this`. If `!ok()`, preserves the current status, but may augment with additional information about `new_status`.

Convenient way of keeping track of the first error encountered. Instead of: `if (overall_status.ok()) overall_status = new_status` Use: `overall_status.Update(new_status);`

### `string tensorflow::Status::ToString() const` <a id="string_tensorflow_Status_ToString"></a>

Return a string representation of this status suitable for printing. Returns the string `"OK"` for success.

### `return tensorflow::Status::OK()` <a id="return_tensorflow_Status_OK"></a>

