# Breaking Down the Code

#1. SHA-256 Implementation

#The program includes a full SHA-256 hashing function, implemented manually instead of using a built-in cryptographic library. This consists of:

#Bitwise right rotation (rightRotate) – A helper function used in SHA-256 transformations.
sha256_transform function – Processes 512-bit (64-byte) blocks of data according to the SHA-256 algorithm.

#sha256 function – The main hashing function that:
Pads the input data according to the SHA-256 specification.
Processes the data in 64-byte chunks.
Outputs the final 32-byte (256-bit) hash.

#2. Data Download using libcurl

#The program fetches data from a URL using libcurl:

#write_data function – Handles incoming data and stores it in a buffer.
#download_data function – Sets up and executes the HTTP request using curl_easy_perform(), writing the downloaded content into a provided buffer.

#3. Main Execution (main function)
#A URL (url[]) is specified for data retrieval.
#A large buffer (data[1000000]) is allocated to store the downloaded content.
#The SHA-256 hash of the fetched data is computed and printed in hexadecimal format.

#Code Execution Steps

#Download Data: The program requests the content from "https://quod.lib.umich.edu/cgi/r/rsv/rsv-idx?type=DIV1&byte=4697892".
#Compute SHA-256 Hash: The downloaded data is passed through the SHA-256 hashing algorithm.
#Print Hash: The computed SHA-256 hash is printed as a hexadecimal string.
#Potential Issues
#Buffer Size Handling (data[1000000]):

#The buffer is fixed at 1 MB. If the downloaded content exceeds this, it may lead to truncation or buffer overflow.
Should dynamically allocate memory instead.
Error Handling for libcurl

#The program does not check if the download succeeded (curl_easy_perform should return CURLE_OK).
If the URL is invalid or unreachable, it may result in an unhandled error.
Insecure Hash Display

#If using SHA-256 for security purposes, simply printing it in printf("%02x") may not be ideal without proper verification.
#Improvements
#Dynamically allocate memory instead of a fixed buffer.
#Check HTTP response codes to handle errors properly.
#Use OpenSSL or another cryptographic library instead of manual SHA-256 implementation for better performance and security.

#Summary
Downloads a file from a URL
Computes and prints its SHA-256 hash
Uses libcurl for HTTP and a custom SHA-256 implementation
