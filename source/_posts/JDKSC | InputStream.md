---
title: Java Doc - InputStream
date: 2023-05-31 08:35
category: Java
---
```JSON
{
    "author": "Arthur van Hoff", 
    "editor": "Sbriny Moon"
}
```
<!--more-->
```JAVA
/**
    InputStream is an abstract class, it is the superclass of all classes representing an input stream of bytes.
    Applications that need to define a subclass of InputStream must always provide a method that returns the next byte of input.
    It has some static final fields:
    1. MAX_SKIP_BUFFER_SIZE  is used to determine the maximum buffer size to use when skipping.
    2. MAX_BUFFER_SIZE is the maximum size of array to allocate. Because some VMs reserve some header words in an array, so attempts to allocate larger arrays may result in OutOfMemoryError: Requested array size exceeds VM limit.

    It has a default no-param-constructor for subclasses to call.
    Next, the function nullInputStream returns a new InputStream that reads no bytes, that whick contains no bytes on InputStream. The returned stream is initially open. The stream is closed by calling the close() method. Subsequent calls to close() have no effect.
    While the stream is open, the avaiable(), read(), read(byte[]), read(byte[],int,int), readAllBytes(), readNBytes(byte[],int,int), readNBytes(int), skip(long), skipNBytes(long), transferTo() methods all behave as is end of stream has been reached. After the stream has been closed, these methods all throw IOException.
    The markSupported() method returns false. The mark() method does nothing, and the reset() method throws IOException.
    InputStream class has only one abstract function that is read(). The funciton read() return the next byte of data, or -1 if the end of the stream is reached. It reads the next byte of data from the input stream. The value byte is returned as an int int the range 0 to 255. If no byte is avaiable because the end of the stream has been reached, the  value -1 is returned. This method blocks until input data is avaiable, the end of the stream is detected, or an exception is thrown.

    The function read() has others implements. It could read the buffer(called b) into whick the data is read and return the total number of bytes read into the buffer, or EOF(End of File) returns -1. Reads some number of bytes from the input stream and stores them into the buffer array b. The number of bytes actually read is returned as an integer. This methos blocks until input data is avaiable, end of file is detected, or an exception is thrown.
    If the length of b is zero, then no bytes are read and 0 is returned, otherwise, there is an attempt to read at least on byte. If no byte is avaiable because the stream is at the end of the file(return -1), otherwise, at least on byte is read and stored into b.
    THE first byte read is stored into element b[0], the next on into b[1], and so on. The number of bytes read is, at most, equal to the length of b. Let k be the b[0] through b[k-1], leaving elements b[k] through b[b.length-1] unaffected.
    The read(b) method for class InputStream has the same effect as: read(b, 0, b.length). If the first byte cannot be read for any reason other than the end of the file, if the inpput stream has been closed, or if some other I/O error accurs, and if code b is null, throws NullPorinterException.

    Reads up to len bytes of data from the input stream into an array of bytes. An attempt is made to read as many as len bytes, but a smaller number may be read. The number of bytes actually read is returned as an integer.
    This method blocks until input data is avaiable, end of file is detected, or an exception si thrown.
    The first bye read is stored into element b[off], the next one into b[off+1], and so on. The number of bytes read is, at most, equal to len. Let k bo the number of bytes actually read; these byets will be stored in elements b[off] through b[off+k-1], leaving elements b[off+k] through b[off+len-1] unaffected.
    In every case, elements b[0] through b[off-1] and elements b[off+lean] through b[b.length-1] are unaffected.
    The read(b, off, len) method for class InputStream simply calls the method read() repeatedly. If the first such call results in an IOException, taht exception is returned from the call to the read(b, off len) method. If any subsequent call to read() results in an IOException, the exception si caught and treated as if it were end of file; the bytes read up to that point are stored into b and the number of bytes read before the exception occurred is returned. The default implementation of this method blocks until the requested amount of input data len has been read, end of file is detected, or an exception is thrown. Subclasses are encouraged to provide a more efficient implementation of this method.
    This function has three params: b - the buffer into which the data is read, off - the start offset in array b at which the data is written, len - the maximum number of bytes to read, finally return the total number of bytes read into the buffer, or -1 if there is no more data because the end of the stream has been reached. 
    If the first byte cannot be read for any reason other than end of file, or if the input stream has been closed, or if some other I/O error occurs can cause IOException, if b is null can cause NullPointer Exception, and if off is negative, len isnegative, r len is greater than b.length-off can cause IndexOutOfBounds Exception.

    A stream needs to read up to a specified number of bytes from the input stream, or intended for simple cases where it is convenient to read all bytes into a byte array.
        1. The function readAllBytes() since 9 reads all remaining bytes from the input stream. This method blocks until all remaining bytes have been read and end of stream is detected, or an Exception is thrown. This method does not close the input stream.
        When this stream reaches end of stream, further invocations of this method will return an empty byte array. 
        Note that this method is intended for simple cases where it is convenient to read all bytes into a byte array. It is not intended for reading input streams with large amounts of data.
        The behavior for the case where the input stream is asyonchronously closed, or the thread interrupted during the read, is highly input stream specific, and therefore not specified.
        If an I/O error occurs reading from the input stream, then it may do so after some, but not all, bytes have been read. Consequently the input stream may not be at end of stream and my be in an inconsistent state. It is strongly recommended that the stream be promptly closed if an I/OC error occurs.
        This method invokes readNBytes(int) with a length of Integer max value, it returns a byte array containing the bytes read from this input stream, if an I/O error occurs throws IOEXception, and if an array of the required size cannot be allocated.
        2. So the readNBytes() method (since 11) reads up to a specified number of bytes from the input stream. This method also has blocks and return case same to the reads.
        The length of the returned array equals the number of bytes read from the stram. If len is zero, then no bytes are read and an empty byte array is returned. Otherwise, up to len bytes are read from the stream. Fewer than len bytes may be read if end of stream is encountered.
        When this stream reaches end of stream, further invocations of this method will return an empty byte array.
        Note that this method is intended for simple cases where it is convenient to read the specified number of bytes into a byte array. The total amount of memory allocated by yhis method is proportional to the number bytes read from the stream which is bounded by len. Therefore, the method may be safely called with very large alues of len provided sufficient memory is available.
        The behavior for the case where the input stream is asynchronously closed, ot the thread interrupted during the read, is highly input stream spcific, and therefore not specified.
        This method has one param - len, it is the maximum number of bytes to read.
        If length is negative cause IllegalArgumentException, if an I/O error occurs cause IOException, and if an array of the required size cannot be allocated.
        If an I/O error occurs reading from the input stream, then it may do so after some, but not all, bytes have been read. Consequently, the input stream my not be at end of stream and my be in an inconsistent state. Alse recommend closed.
        The number of bytes allocated to tead data from this stream and return the reasult is bounded by 2*(long)len, inclusive.
        3. Another readNBytes has more params, they are b - the byte array into which the data is read, off - the start offset in b at which the data is written, and len - the maximum number of bytes to read, this method return the actual number of bytes read into the buffer.
        This readNBytes method since 9, it reads the requested number of bytes from the input stream into the given byte array. It also has blocks, and return cases(0,-1).
        In the case wherer end of stream is reached before len bytes have been read, the nthe actual number of bytes read will be returned.
        If len is zero, then no bytes are read and 0 is returned. Otherwise, there is an attempt to read up to len bytes.
        The first byte read is stored into element b[off], the next one in to b[off+1], and so on. The number of bytes read is, at most,equal to len. Let k be the number of bytes actually read, these bytes will be stored in elements b[off] through b[off+k-1], leaving elements b[off+k] through b[off+len-1] unaffected.
        The behavior for the case where the input stream is asynchronousely closed, or the thead interrupted during the read, is highly input stream specific, and therefore not specified.
        If an I/O error occurs method throws IOException, if b id null can cause NullPointerException, and if off is negative or len is negative is negative, or len is greater than b.length-off can cause IndexOutOfBoundsException.

    A stream needs overlook some bytes data while using skip method. Method skip and skipNBytes can skip over and discards exactly n bytes of data from this input stream.
        1. The skip method has one param n, it is the nubmer of bytes to be skipped, and return the actual number of bytes skipped which might be sero.
        The skip method may, for a variety of reasons, end up skipping over some smaller number of bytes, possibly 0. This may result from any of a number of conditions, reaching end of file before n bytes have been skipped is only one possibility.
        The actual number of bytes have been skipped is only one possibility. The actual number of byte skipped is returned. If n is negative, the skip method for class InputStream always returns 0, and no bytes are skipped. Subcalsses may handle the negative value differently.
        The skip method implementation of this class creates a byte array and then repeatedly reads into it until n bytes have been read or the end of the stream has been reached. Subclasses are encouraged to provide a more efficient implementation of this method. For instance, the implementation may depend on the ability to seek.
        If an I/O error occurs caused IOException.
        2. The skipNBytes method has one param n, it is the number of bytes to be skipped, since 12.
        If n is zero or negative, then no bytes are skipped. If n is positive, the default implementation of this method invokes skip(long) repeatedly with its parameter equal to the remaining number of bytes to skip until the requested number of bytes has been skipped or an error condition occurs. If at any point the return value of skip() is negative or greater than the remaining number of bytes to be skipped, then an IOException is thrown.
        If skip() ever returns zero, then read() is invoked to read a single byte, and if it returns -1, then an EOFException is thrown. Any excpetion thrown by skip() or read() will be propagated.
        Subclasses are encouraged to provide a more efficient implementation of this method.
        If end of stream is encountered before the stream can be positioned n bytes beyond its position when this method was invoked could cause cause EOFExcepiton, and if the stream cannot be positioned properly or if an I/O error occurs could cause IOException.

    Method available return an estimate of the number of bytes that can be read (or skipped over) from this input stream without blocking or 0 when it reaches the end of the input stream.
    The read might be on the same thread or another thead. A single read or skip of this may bytes will not block, but may read or skip fewer bytes.
    Note that while some implementations of InputStream will return the total number of bytes in the stream, many will not. It is never correct to use the return value of this method to allocate a buffer intended to hold all data in this stream.
    A subclass's implementation of this method may choose to throw an IOException if this input stream has been closed by invoking the close() method.
    In abstact class InputStream, the avaiable method alwats returns 0, this method should be overridden by subclasses.

    Method close of InputStream does noting, close this input stream and releases any system resources associated with the stream. 

    A stream needs repositions to the position at the time the mark method was last called on this input stream.
        1. Method markSupported test if the input stream supports the mark and reset methods. Whether or not mark and reset are supported is an invariant property of a particular input stream instance. The markSupported method of InputStream returns false, if the stream instance suports the mark and reset methods, otherwise return false.
        2. Method mark marks the current position in this input stream, it has one param readlimit, it is the maximum limit of bytes that can be read before the mark position becomes invalid. The readlimit arguments tells this input stream to allow that many bytes to be read before the mark position gets invalidated.
        A subsequent call to the reset method repositions this stream at the last marked position so that subsequent reads re-read the same bytes.
        The general contract of mark is that, if the method markSupported returns true, the stream somehow remembers all the bytes read after the call to mark and stands ready to supply those same bytes again if and whenever the method reset is called. However, the stream is not required to remember any data at all if more than readlimit bytes are read from the stream before reset is called.
        This method marking a closed stream should not have any effect on the stream, the mark method of InputStream does nothing.
        3. Method reset repositions the stream to the position at the time the mark method was last called on this input stream. The general contract of reset is :
        If the method markSupported returns true, then:
        If the method mark has not been called since the stream was created, ot the number of bytes read from the stream since mark was last called is larger than the argument to mark at that last call, the nan IOException might be thrown. 
        If such an IOException is not thrown, then the stream is reset to a state such that all the bytes read since the most recent call to mark (or since the start of the file, if mark has not been called) will be resupplied to subsequent callers of the read method, followed by any bytes that otherwise would have been the next input data as of the time of the call to reset.
        If the methos markSupported return false, then:
        The call to reset may throw on IOException.
        If an IOException si not thrown, then the stream is reset to a fixed state that depends on the particular type of the input stream and how it was created. The bytes that will be supplied to subsequent callers of the read method depend on the particular type of the input steam.
        method reset for class InputStream does noting except throw on IOException.
        If the (instance)stream has not been marked or if the mark has been invalidated, throws IOException.

    Method transferTo has one param out, it is the output stream, non-null, and return the number of bytes transferred.
    Reads all bytes from this input stream and writes the bytes to the given output stream in the order that they are read. On return, this input stream will be at end of stream. This method does not close either stream.
    This method may block indefinitely reading from the input stream, or writing to the output stream. The behavior for the case where the input and/or output stream is asynchronously closed, or the thread interrupted during the transfer, is highly input and output stream specific, and therefore not specified.
    If an I/O error occurs reading from the input stream or writing to the output stream, then it may do so aftersome bytes have been read or written. Consequently the input stream may not be at end of stream and on, or both, streams may be in an inconsistent state. It is strongly recommended that both streams be promptly closed if an I/O error occurs.
 */
```