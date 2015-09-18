#!/usr/bin/env python

def KSA(key):
    keylength = len(key)

    S = list(range(256))

    j = 0
    for i in range(256):
        j = (j + S[i] + key[i % keylength]) % 256
        S[i], S[j] = S[j], S[i]  # swap

    return S


def PRGA(S):
    i = 0
    j = 0
    while True:
        i = (i + 1) % 256
        j = (j + S[i]) % 256
        S[i], S[j] = S[j], S[i]  # swap

        K = S[(S[i] + S[j]) % 256]
        yield K


def RC4(key):
    S = KSA(key)
    return PRGA(S)


if __name__ == '__main__':
    # test vectors are from http://en.wikipedia.org/wiki/RC4

    # ciphertext should be BBF316E8D940AF0AD3
    key = 'Key'
    plaintext = 'Plaintext'

    # ciphertext should be 1021BF0420
    #key = 'Wiki'
    #plaintext = 'pedia'

    # ciphertext should be 45A01F645FC35B383552544B9BF5
    #key = 'Secret'
    #plaintext = 'Attack at dawn'

    def convert_key(s):
        return [ord(c) for c in s]
    key2 = convert_key(key)

    keystream = RC4(key2)

    import sys
    for c in plaintext:
        #sys.stdout.write("%02X" % (ord(c) ^ next(keystream)))
        n1 = ord(c)
        keystream = RC4([ ord(x) for x in key])
        ks1 = next(keystream)
        n2 = n1 ^ ks1
        n3 = n2 ^ ks1
        c2 = chr(n3)
        sys.stdout.write("%s" % c2)

    print


#!/usr/bin/env python

def KSA(key):
    keylength = len(key)

    S = list(range(256))

    j = 0
    for i in range(256):
        j = (j + S[i] + key[i % keylength]) % 256
        S[i], S[j] = S[j], S[i]  # swap

    return S


def PRGA(S):
    i = 0
    j = 0
    while True:
        i = (i + 1) % 256
        j = (j + S[i]) % 256
        S[i], S[j] = S[j], S[i]  # swap

        K = S[(S[i] + S[j]) % 256]
        yield K


def RC4(key):
    S = KSA(key)
    return PRGA(S)


if __name__ == '__main__':
    # test vectors are from http://en.wikipedia.org/wiki/RC4

    # ciphertext should be BBF316E8D940AF0AD3
    key = 'Key'
    plaintext = 'Plaintext'

    # ciphertext should be 1021BF0420
    #key = 'Wiki'
    #plaintext = 'pedia'

    # ciphertext should be 45A01F645FC35B383552544B9BF5
    #key = 'Secret'
    #plaintext = 'Attack at dawn'

    def convert_key(s):
        return [ord(c) for c in s]
    key2 = convert_key(key)

    keystream = RC4(key2)

    import sys
    for c in plaintext:
        #sys.stdout.write("%02X" % (ord(c) ^ next(keystream)))
        n1 = ord(c)

        #init the key generator
        keystream = RC4([ ord(x) for x in key])
        encoded = [ (ord(x) ^ next(keystream)) for x in plaintext ]

        # gotta reset it
        keystream = RC4([ ord(c) for c in key])
        decoded = [ (x ^ next(keystream)) for x in encoded ]
        [ chr(x) for x in decoded ]
        

    sys.stdout.write("%s" % ''.join([ chr(x) for x in decoded ]))

    print
