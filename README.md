# gc_apple_keys
# This is Guide To generate certificates for Apple pay with Georgian Card
# Generate merchant key

openssl req -sha256 -nodes -newkey rsa:2048 -keyout merchant.identity.pk.pem -out merchant.identity.request.csr


openssl pkcs8 -v1 PBE-SHA1-3DES -topk8 -in merchant.identity.pk.pem -out merchant.identity.pk.ENCRYPTED.pem;
# upload merchant.identity.request.csr to  https://developer.apple.com/  on Apple Pay Merchant Identity Certificate, download signed cer File

openssl x509 -inform der -in merchant_id.cer -out merchant.identity.pem

# Payment processing csr and encrypted private key:

# generate payment key and certificate
openssl ecparam -out payment.processing.private.key -name prime256v1 -genkey
openssl req -new -sha256  -key payment.processing.private.key  -nodes -out payment.processing.reqauest.csr
openssl pkcs8 -topk8 -in payment.processing.private.key  -out payment.processing.pk.ENCRYPTED.pem

# upload payment.processing.reqauest.csr to  https://developer.apple.com/  on Apple Pay Payment Processing Certificate, download signed cer File
openssl x509 -inform der -in apple_pay.cer -out payment.processing.pem

# send this files to Gorgian Card

# merchant.identity.pk.ENCRYPTED.pem
# merchant.identity.pem
# payment.processing.pk.ENCRYPTED.pem
# payment.processing.pem







