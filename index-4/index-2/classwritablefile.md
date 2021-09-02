# class tensorflow::WritableFile

A file abstraction for sequential writing.

The implementation must provide buffering since callers may append small fragments at a time to the file.

## Member Details

### `tensorflow::WritableFile::WritableFile()` <a id="tensorflow_WritableFile_WritableFile"></a>

### `tensorflow::WritableFile::~WritableFile()` <a id="tensorflow_WritableFile_WritableFile"></a>

### `virtual Status tensorflow::WritableFile::Append(const StringPiece &data)=0` <a id="virtual_Status_tensorflow_WritableFile_Append"></a>

### `virtual Status tensorflow::WritableFile::Close()=0` <a id="virtual_Status_tensorflow_WritableFile_Close"></a>

### `virtual Status tensorflow::WritableFile::Flush()=0` <a id="virtual_Status_tensorflow_WritableFile_Flush"></a>

### `virtual Status tensorflow::WritableFile::Sync()=0` <a id="virtual_Status_tensorflow_WritableFile_Sync"></a>

