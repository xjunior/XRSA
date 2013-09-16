XRSA
==========

Let's make it clear: the main part of this code wasn't written by me. Everything was found on the following URL:

http://blog.iamzsx.me/show.html?id=155002

Unfortunately I've seen this code being distributed through StackOverflow and Blog posts. That's POS. I'm just
taking the job of making it into a proper repository and distribute it as a pod. Feel free to log bugs and
send pull requests, I'll make sure to tackle them.

If you want a good tutorial of how to use it, you can find it here in english:

http://jslim.net/blog/2013/01/05/rsa-encryption-in-ios-and-decrypt-it-using-php/

Follows a copy and paste of that:

RSA Encryption in iOS:

1) generate a key-pair using SSL.

    openssl req -x509 -out public_key.der -outform der -new -newkey rsa:1024 -keyout private_key.pem -days 3650

There are few points have to mention:

* public_key.der is an output based on x509 certificate. Note that in iOS must be .der format but not .pem
* private_key.pem is the private key that you can use it to decrypt
* rsa:1024 is the key length. The longer the length, the safer it is
* -days is the days for effective period for this cert. In this case, is 10-Years

2) Now, drag public_key.der to your iOS

3) To encrypt data, this is how you do:

    NSString *keyPath = [[NSBundle mainBundle] pathForResource:@"public_key" ofType:@"der"];
    XRSA *rsa = [[XRSA alloc] initWithPublicKey:keyPath];
    if (rsa != nil) {
        NSLog(@"%@", [rsa encryptToString:@"This is plaintext"]);
    } else {
        NSLog(@"Error");
    }

