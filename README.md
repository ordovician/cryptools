# Cryptools

A collection of small command line tools written in Go for learning about encoding binary data in different formats such as base32 and base64. How to work with the encryption algorithms for encryption, decryption and key management.

To build the different commands you can run the go build command:

    ❯ go build ./cmd/generate
    ❯ go build ./cmd/encoder
    ❯ go build ./cmd/decrypt
    ❯ go build ./cmd/encrypt

Here are some examples of usage. This creates a random key and stores it in base64 format. You can use this key with the encryption and decryption commands.

    ❯ ./generate -keylen 16 -encoding base64 > key.txt
    ❯ cat key.txt
    OKn9kRVk97GfeSl/2UaaUg=
    
    
All the commands have a `-h` and `-help` swith to get info on how to use them

    ❯ ./generate -h
    Usage of ./generate:
      -encoding string
        	Encoding to use for key. Could be hex, base32, base64 or pem (default "hex")
      -keylen int
        	Length of encryption key (default 16)
            
Let us use the key to encrypt and decrypt a message:

    ❯ echo "hello world" > message.txt
    ❯ ./encrypt -encoding base64 -key key.txt message.txt > secret.txt
    ❯ cat secret.txt
    PFLRBIRCMOCE25GOCYHXLTXR2MSS3J3MQ2CP3QOTENFMEUZAO4LA====⏎
    ❯ ./decrypt -encoding base64 -key key.txt  secret.txt
    hello world
    
You need to use the `-encoding` swith otherwise the program will not know how the key file was encoded, and then it cannot read the AES encryption key.
