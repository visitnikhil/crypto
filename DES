#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/dsa.h>
#include <openssl/sha.h>

int main() {
    DSA *dsa = DSA_generate_parameters(1024, NULL, 0, NULL, NULL, NULL, NULL);
    if (!dsa) {
        fprintf(stderr, "DSA key generation failed.\n")
        return 1;
    }

    DSA_generate_key(dsa);

    const char *message = "Hello, DSA!";
    unsigned char digest[SHA_DIGEST_LENGTH];
    SHA1((const unsigned char *)message, strlen(message), digest);

    DSA_SIG *signature = DSA_do_sign(digest, SHA_DIGEST_LENGTH, dsa);

    if (DSA_do_verify(digest, SHA_DIGEST_LENGTH, signature, dsa)) {
        printf("DSA Signature Verification: Valid\n");
    } else {
        printf("DSA Signature Verification: Invalid\n");
    }

    DSA_free(dsa);
    DSA_SIG_free(signature);

    return 0;
}
