---
description: Use of JWE to ensure payload security and integrity
---

# Message Security and Integrity

TO ensure that sensitive information in the actual domain objects is not accessible even to the HCX, protocol requires the payload defined by the domain data specifications to be encrypted using a separate asymmetric encryption key of the final recipient established at the time of participant onboarding into the registry. API then carries the encrypted value of the payload. The payload encryption is expected to be performed using JSON web encryption [RFC7516](https://datatracker.ietf.org/doc/html/rfc7516) as per algorithm and enclosed values fixed in the **protected headers** section above. At this point in time, no unprotected headers are envisioned in the HCX protocol. We also do not envision multiple recipient delivery in the current version of the HCX protocol.

## **Message Encryption**

The high-level steps to encrypt the payload using the public key of the final recipient are:

1. Find out the public key of the recipient through registry lookup on HCX.
2. Let JWE protected header be = BASE64URL(UTF8((Registered JOSE headers) U (HCX Protocol Headers) U (HCX Domain Headers)). Please note that initial version of HCX protocol requires following JOSE headers: {"alg":"RSA-OAEP","enc":"A256GCM"}
3. Generate a random Content Encryption Key (CEK) as per the encryption algorithm.
4. Encrypt the CEK with the recipient's public key using the RSAES-OAEP algorithm to produce the JWE Encrypted Key.
5. Base64url-encode the JWE Encrypted Key.
6. Generate a random JWE Initialization Vector.
7. Base64url-encode the JWE Initialization Vector.
8. Let the Additional Authenticated Data encryption parameter be

ASCII(BASE64URL(UTF8(JWE Protected Header))).

1. Perform authenticated encryption on the plaintext with the AES GCM algorithm using the CEK as the encryption key, the JWE Initialization Vector, and the Additional Authenticated Data value, requesting a 128-bit Authentication Tag output.
2. Base64url-encode the ciphertext.
3. Base64url-encode the Authentication Tag
4. Assemble the final representation in flattened JSON serialization (Section 7.2.2 of [RFC7516](https://datatracker.ietf.org/doc/html/rfc7516)):

```
{
  "protected":"<integrity-protected header contents from step 2 above>",
  "encrypted_key":"<encrypted key contents from step 5 above>",
  "aad":"<additional authenticated data contents from step 8 above>",
  "iv":"<initialization vector contents from step 7 above>",
  "ciphertext":"<ciphertext contents from step 10 above>",
  "tag":"<authentication tag contents from step 11 above>"
}
```

## **Message Decryption**

The high-level steps to decrypt and verify the integrity of the payload using the private key of the final recipient are:

1. From the received JSON serialized JWE token, Base64url decode the encoded representations of the JWE Protected Header (protected), the JWE Encrypted Key (encrypted\_key), the JWE Initialization Vector (iv), the JWE Ciphertext (ciphertext), the JWE Authentication Tag (tag), and the JWE AAD (aad), following the restriction that no line breaks, whitespace, or other additional characters have been used.
2. Verify that the octet sequence resulting from decoding the encoded JWE Protected Header is a UTF-8-encoded representation of a completely valid JSON object conforming to [RFC 7159](https://datatracker.ietf.org/doc/html/rfc7159); let the JWE Protected Header be this JSON object.
3. Let the JOSE Header be the JWE Protected Header. Verify that the resulting JOSE Header does not contain duplicate Header Parameter names.
4. Determine the Key Management Mode employed by the algorithm specified by the "alg" (algorithm) Header Parameter.
5. Verify that the JWE uses a key known to the recipient.
6. Decrypt the JWE Encrypted Key to produce the CEK. The CEK MUST have a length equal to that required for the content-encryption algorithm.
7. Compute the Encoded Protected Header value BASE64URL(UTF8(JWE Protected Header)). This protected header is (Registered JOSE headers) U (HCX Protocol Headers) U (HCX Domain Headers).
8. Let the Additional Authenticated Data encryption parameter be ASCII(Encoded Protected Header).
9. Decrypt the JWE Ciphertext using the CEK, the JWE Initialization Vector, the Additional Authenticated Data value, and the JWE Authentication Tag (which is the Authentication Tag input to the calculation) using the specified content-encryption algorithm, returning the decrypted plaintext and validating the JWE Authentication Tag in the manner specified for the algorithm, rejecting the input without emitting any decrypted output if the JWE Authentication Tag is incorrect.

Participating systems are expected to follow best practices guidelines as in [RFC8725](https://datatracker.ietf.org/doc/html/rfc8725) to ensure the security of the payload.

It is recommended to rotate these encryption keys once every year and mechanisms implemented for the providers/payers/HCX to intimate the ecosystem about the potential compromise of the keys.

Here is a sample of the set of libraries that you can explore:

1. Bouncy castle
2. Openssl
3. NaCl
4. Libgcrypt
5. PyNaCl
6. TweetNaCl
