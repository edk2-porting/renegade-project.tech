# sectools

```
usage: sectools [-h] [--version] [--open-source-licenses] feature ...

Qualcomm Security Tools v1.27

Optional Arguments:
  -h, --help            Show this help message and exit.
  --version             Show tool version and exit.
  --open-source-licenses
                        Print the licenses of all included open source code and exit.

Required Arguments:
  feature               secure-image, metabuild-secure-image, secure-debug, tme-secure-debug, fuse-blower, fuse-validator, elf-tool, elf-consolidator, or mbn-tool

For help menu of a specific feature: sectools <feature> -h
```

# sectools secure-image

```
usage: sectools secure-image [infile]
                             [-h] [-v] [--signing-help] [--available-signature-formats] [--encryption-help] [--available-encryption-formats] [--available-device-restrictions]
                             [--available-image-ids] [--available-variants] [--vouch-for VOUCH_FOR [VOUCH_FOR ...]] [--image-id IMAGE_ID [IMAGE_ID ...]]
                             [--fuse-blower-images FUSE_BLOWER_IMAGES [FUSE_BLOWER_IMAGES ...]] [--outfile OUTFILE] [--compressed-outfile COMPRESSED_OUTFILE] [--outfile-record OUTFILE_RECORD]
                             [--pil-split-outdir PIL_SPLIT_OUTDIR] [--security-profile SECURITY_PROFILE [SECURITY_PROFILE ...]] [--inspect] [--dump DUMP] [--verify-root VERIFY_ROOT]
                             [--validate] [--sign] [--hash] [--encrypt] [--compress] [--persist-sections] [--pil-split] [--segment-hash-algorithm {SHA256,SHA384,SHA512}] [--qti]
                             [--signature-format SIGNATURE_FORMAT] [--signing-mode {LOCAL,TEST,PLUGIN,CASS,QTI-REMOTE}] [--root-certificate ROOT_CERTIFICATE [ROOT_CERTIFICATE ...]]
                             [--root-key ROOT_KEY] [--ca-certificate CA_CERTIFICATE] [--ca-key CA_KEY] [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT]
                             [--root-certificate-count {1,2,3,4}] [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT] [--plugin-signer PLUGIN_SIGNER]
                             [--plugin-signer-args PLUGIN_SIGNER_ARGS] [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT] [--cass-capability CASS_CAPABILITY]
                             [--cass-password CASS_PASSWORD] [--cass-password-file CASS_PASSWORD_FILE] [--cass-token-serial-number CASS_TOKEN_SERIAL_NUMBER] [--cass-capability CASS_CAPABILITY]
                             [--qti-remote-signing-server-url QTI_REMOTE_SIGNING_SERVER_URL] [--qti-remote-signing-server-port QTI_REMOTE_SIGNING_SERVER_PORT]
                             [--root-key-type {RTL-QTI,OTP-OEM,OTP-QTI}] [--encryption-format ENCRYPTION_FORMAT] [--encryption-mode {LOCAL,TEST,PLUGIN,QTI-REMOTE}] [--l1-key L1_KEY]
                             [--l2-key L2_KEY] [--l3-key L3_KEY] [--data-encryption-key DATA_ENCRYPTION_KEY] [--device-public-key DEVICE_PUBLIC_KEY [DEVICE_PUBLIC_KEY ...]]
                             [--encrypted-segment-index ENCRYPTED_SEGMENT_INDEX [ENCRYPTED_SEGMENT_INDEX ...]] [--plugin-encrypter PLUGIN_ENCRYPTER]
                             [--plugin-encrypter-args PLUGIN_ENCRYPTER_ARGS] [--qti-remote-encryption-server-url QTI_REMOTE_ENCRYPTION_SERVER_URL]
                             [--qti-remote-encryption-server-capability QTI_REMOTE_ENCRYPTION_SERVER_CAPABILITY]
                             [--platform-binding {SOC-HW-VER,JTAG-ID,SOC-FEATURE-ID,PRODUCT-SEGMENT-ID,INDEPENDENT} [{SOC-HW-VER,JTAG-ID,SOC-FEATURE-ID,PRODUCT-SEGMENT-ID,INDEPENDENT} ...]]
                             [--variant VARIANT] [--serial-number SERIAL_NUMBER [SERIAL_NUMBER ...]] [--oem-id OEM_ID] [--oem-product-id OEM_PRODUCT_ID]
                             [--anti-rollback-version ANTI_ROLLBACK_VERSION] [--root-certificate-index {0,1,2,3}] [--transfer-root]
                             [--measurement-register-target {HMR1,HMR2,FMR1,FMR2,FMR3,FMR4}] [--oem-lifecycle-state {DEVELOPMENT,PRODUCTION}]
                             [--oem-root-certificate-hash OEM_ROOT_CERTIFICATE_HASH] [--soc-lifecycle-state {RMA,OPERATIONAL-EXT,OPERATIONAL-INT} [{RMA,OPERATIONAL-EXT,OPERATIONAL-INT} ...]]
                             [--jtag-debug {NOP,ENABLE,DISABLE}] [--secondary-software-id SECONDARY_SOFTWARE_ID] [--feature-id FEATURE_ID] [--client-id CLIENT_ID] [--library-id LIBRARY_ID]
                             [--transfer-uie-key] [--crash-dump]

Tool for signing, encrypting, and inspecting Qualcomm software images.

Help:
  -h, --help            Show this help message and exit.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.
  --signing-help        Show signing options and exit.
  --available-signature-formats
                        Show available --signature-format values and exit. Must be used with --security-profile.
  --encryption-help     Show encryption options and exit.
  --available-encryption-formats
                        Show available --encryption-format values and exit. Must be used with --security-profile.
  --available-device-restrictions
                        Show available device restrictions when performing the --sign, --hash, or --encrypt operations.
  --available-image-ids
                        Show available --image-id values and exit. Must be used with --security-profile.
  --available-variants  Show available --variant values and exit. Must be used with --security-profile.

Image Inputs:
  infile                File path of input software image.
  --vouch-for VOUCH_FOR [VOUCH_FOR ...]
                        File path of image(s) to be added to a new or existing Multi Image. --outfile will be a Multi Image and will contain the hashes of the --vouch-for images. infile is
                        optional in this mode. If infile is provided, it must be a Multi Image. If infile is not provided, a new Multi Image will be created.
  --image-id IMAGE_ID [IMAGE_ID ...]
                        ID of infile when --sign, --hash, --encrypt, or --validate is provided. ID(s) of image(s) provided via --vouch-for when adding entries for images to Multi Image.
  --fuse-blower-images FUSE_BLOWER_IMAGES [FUSE_BLOWER_IMAGES ...]
                        Fuse Blower Images (typically named sec.elf or sec.dat) whose fuse values will be cross checked against the image being validated when performing the --validate
                        operation.

Image Outputs:
  --outfile OUTFILE     File path of output software image.
  --compressed-outfile COMPRESSED_OUTFILE
                        File path of compressed output software image. Must only be used when performing --compress in addition to the --sign, --hash, or --encrypt operations. If provided,
                        uncompressed output software image will be stored at --outfile. If not provided when performing --compress, compressed output software image will be stored at --outfile.
  --outfile-record OUTFILE_RECORD
                        File path of JSON file recording Image ID and location of OEM-signed --outfile.
  --pil-split-outdir PIL_SPLIT_OUTDIR
                        Directory at which to store PIL split files. Must be used with --pil-split.

Security Profile:
  --security-profile SECURITY_PROFILE [SECURITY_PROFILE ...]
                        File path of one or more Security Profile XMLs. A Security Profile describes the security features of a Qualcomm chipset.

Image Operations:
  --inspect             Print infile in a human-readable format.
  --dump DUMP           Decompose infile and store its regions at the specified directory.
  --verify-root VERIFY_ROOT
                        Root certificate hash to verify against the root certificate(s) of infile.
  --validate            If provided along with --outfile, validates --outfile against the --security-profile and any provided --fuse-blower-images. If --outfile is not provided, validates that
                        infile is compatible with the --security-profile and any provided --fuse-blower-images.
  --sign                Add or replace the signature and certificate chain of infile or newly generated Multi Image.
  --hash                Add or replace the Hash Table Segment of infile or newly generated Multi Image.
  --encrypt             Encrypt infile or newly generated Multi Image. If infile is already signed and hashing and signing is not being performed along with encryption, infile's preexisting
                        signature(s), certificate chain(s), and device restrictions will be persisted.
  --compress            Compress infile or newly generated --outfile.

Image Format:
  --persist-sections    Retain all ELF sections of infile. If not provided, all ELF sections of infile will be removed. Must only be used when performing the --sign, --hash, or --encrypt
                        operations.
  --pil-split           PIL split --outfile. If not provided, --outfile will not be PIL split. Can only be used when performing the --sign, --hash, or --encrypt operations. The resulting PIL
                        split files will be saved in the same directory as --outfile if --pil-split-outdir is not provided. The name of the PIL split files will be prefixed with --outfile's
                        file name.
  --segment-hash-algorithm {SHA256,SHA384,SHA512}
                        Defaults to the algorithm specified in the --security-profile. Hash algorithm to use for computing Hash Table Segment hash entries when performing the --hash, --sign, or
                        --encrypt operations.

Authority:
  --qti                 Operate on infile or newly generated Multi Image as Qualcomm. If not provided, defaults to operating in OEM mode.

```

## sectools secure-image --signing-help

```
Signature Format:
  --signature-format SIGNATURE_FORMAT
                        Defaults to the signature format in --security-profile. Denotes the signature format to be used to sign --outfile. To list supported signature formats, provide
                        --available-signature-formats.

Signing Mode:
  --signing-mode {LOCAL,TEST,PLUGIN,CASS,QTI-REMOTE}
                        If LOCAL, locally provided signing keys and certificates are used to generate the signature and certificates. If TEST, Security Tools' prepackaged internal test signing
                        keys and certificates are used to generate the signature and certificates. If PLUGIN, generation of the signature and certificates is off-loaded to --plugin-signer. If
                        CASS, Qualcomm's Code Authorization Signing Service is used to generate the signature and certificates. If QTI-REMOTE, a Qualcomm proxy server is used to generate the
                        signature and certificates via CASS.

Local Signing (INSECURE):
  --outfile will contain a certificate chain of depth 3 when --ca-certificate is provided, else a certificate chain of depth 2. The leaf (Attestation) certificate will be created by the tool.

  --root-certificate ROOT_CERTIFICATE [ROOT_CERTIFICATE ...]
                        File path of one or more root certificates to use for signing.
  --root-key ROOT_KEY   File path of root key. Required if --ca-certificate is not provided.
  --ca-certificate CA_CERTIFICATE
                        File path of CA certificate to use for signing.
  --ca-key CA_KEY       File path of CA key. Required when --ca-certificate is provided.
  --attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT
                        Custom subject string to be included in the Attestation Certificate.

Test Signing (INSECURE):
  Test signing should never be used in production use cases. It is intended only for testing purposes. The private keys used for signing are contained within Security Tools and are available
  to anyone possessing Security Tools.

  --root-certificate-count {1,2,3,4}
                        Number of root certificates to use for signing. Defaults to 1.
  --attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT
                        Custom subject string to be included in the Attestation Certificate.

Plug-in Signing:
  --plugin-signer PLUGIN_SIGNER
                        File path of Python script which implements Plug-in Signer Interface.
  --plugin-signer-args PLUGIN_SIGNER_ARGS
                        Plug-in Signer implementation-specific inputs. --plugin-signer can implement handling of custom input parameters. Those parameters can be provided to --plugin-signer via
                        --plugin-signer-args.
  --attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT
                        Custom subject string to be included in the Attestation Certificate.

CASS Signing:
  --cass-password and --cass-password-file are mutually exclusive.

  --cass-capability CASS_CAPABILITY
                        CASS capability to use for signing. Provided by Qualcomm.
  --cass-password CASS_PASSWORD
                        CASS token password.
  --cass-password-file CASS_PASSWORD_FILE
                        File path of file containing CASS token password.
  --cass-token-serial-number CASS_TOKEN_SERIAL_NUMBER
                        Serial number of the CASS token. Used to identify the correct token when multiple are connected to the same machine. The serial number and additional token information
                        can be found in the SafeNet Authentication Client.

QTI Remote Signing:
  --cass-capability CASS_CAPABILITY
                        CASS capability to use for signing. Provided by Qualcomm.
  --qti-remote-signing-server-url QTI_REMOTE_SIGNING_SERVER_URL
                        URL of QTI Image Signing Server.
  --qti-remote-signing-server-port QTI_REMOTE_SIGNING_SERVER_PORT
                        Port of QTI Image Signing Server.
```

## sectools secure-image --encryption-help

```
Root Key Type:
  --root-key-type {RTL-QTI,OTP-OEM,OTP-QTI}
                        Applicable only to UIE encryption. Defaults to the default_root_key_type in --security-profile. Identifies from where the device should retrieve the L1 decryption key
                        while decrypting --outfile.

Encryption Format:
  --encryption-format ENCRYPTION_FORMAT
                        Defaults to the encryption format in --security-profile. Denotes the encryption format to be used to encrypt --outfile. To list supported encryption formats, provide
                        --available-encryption-formats.

Encryption Mode:
  --encryption-mode {LOCAL,TEST,PLUGIN,QTI-REMOTE}
                        If LOCAL, locally provided encryption keys are used to generate the Encryption Parameters and encrypt --outfile. If TEST, Security Tools' prepackaged internal test
                        encryption keys are used to generate the Encryption Parameters and encrypt OUTFILE. If PLUGIN, generation of the Encryption Parameters is off-loaded to --plugin-
                        encrypter. If QTI-REMOTE, Qualcomm's Image Encryption Server is used to generate the Encryption Parameters.

Local UIE Encrypting (INSECURE):
  --l1-key L1_KEY       File path of L1 key to use for encrypting --l2-key.
  --l2-key L2_KEY       File path of L2 key to use for encrypting --l3-key. If not provided, a randomly generated key will be used.
  --l3-key L3_KEY       File path of L3 key to use for encrypting --outfile's loadable segments. If not provided, a randomly generated key will be used.

Local QBEC Encrypting:
  --data-encryption-key DATA_ENCRYPTION_KEY
                        File path of 256-bit key to use for QBEC XTS encrypting --outfile's encryptable segments. If not provided, a randomly generated key will be used.
  --device-public-key DEVICE_PUBLIC_KEY [DEVICE_PUBLIC_KEY ...]
                        File path of one or more device public keys to use to QBEC encrypt --outfile. Not applicable when operating as --qti.
  --encrypted-segment-index ENCRYPTED_SEGMENT_INDEX [ENCRYPTED_SEGMENT_INDEX ...]
                        Index and/or a range of indices of one or more segments in infile to be QBEC GCM encrypted. When providing a range, it must be of the form <lower_index>-<higher_index>.
                        If not provided, all LOAD segments will be encrypted.

Test Encrypting (INSECURE):
  Applicable only to UIE encryption. Test encryption should never be used in production use cases. It is intended only for testing purposes. The L1, L2, and L3 keys used for encryption are
  contained within Security Tools and are available to anyone possessing Security Tools. The symmetric L1 key's value is 0x6c26d6285ef322ef9ee58104b53496cb. The asymmetric L1 key's value is
  0x8cbd623695ab427530de8745e60d9137a796b5e6b63eb9ebea6e067dfe1addd8b1884298dd8cc3fcb7346accadbb0d9c897637f1fdbd2e05b2f89ce4ccc06f3b.

Plug-in Encrypting:
  Applicable only to UIE encryption.

  --plugin-encrypter PLUGIN_ENCRYPTER
                        File path of Python script which implements Plug-in Encrypter Interface.
  --plugin-encrypter-args PLUGIN_ENCRYPTER_ARGS
                        Plug-in Encrypter implementation-specific inputs. --plugin-encrypter can implement handling of custom input parameters. Those parameters can be provided to --plugin-
                        encrypter via --plugin-encrypter-args.

QTI Remote Encrypting:
  Applicable only to UIE encryption.

  --qti-remote-encryption-server-url QTI_REMOTE_ENCRYPTION_SERVER_URL
                        URL of QTI Image Encryption Server.
  --qti-remote-encryption-server-capability QTI_REMOTE_ENCRYPTION_SERVER_CAPABILITY
                        Capability to use for encrypting. Provided by Qualcomm.
```

# sectools metabuild-secure-image

```
usage: sectools metabuild-secure-image [-h] [-v] [--secure-image-help] [--available-filters] [--available-image-ids] [--available-variants] [--available-signature-formats]
                                       [--available-encryption-formats] [--outfile OUTFILE | --outdir OUTDIR] [--image-finder IMAGE_FINDER] [--image-id IMAGE_ID [IMAGE_ID ...]]
                                       [--chipset CHIPSET] [--flavor FLAVOR] [--storage STORAGE] [--vouch-for][...]

Metabuild Secure Image v1.0. Based on Qualcomm Security Tools v1.27. Tool for performing secure-image operations on a Metabuild's software images.

Help:
  -h, --help            Show this help message and exit.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.
  --secure-image-help   Show secure-image options and exit.
  --available-filters   Show available values for --chipset, --flavor, --storage, --image-id and exit.
  --available-image-ids
                        Show available --image-id values and exit.
  --available-variants  Show available --variant values and exit. Provide along with --chipset to show variants of a specific chipset.
  --available-signature-formats
                        Show available --signature-format values and exit.
  --available-encryption-formats
                        Show available --encryption-format values and exit.

Image Outputs:
  --outfile and --outdir are mutually exclusive.

  --outfile OUTFILE     File path of output software image. Can be provided when one --image-id value or --vouch-for is provided.
  --outdir OUTDIR       Directory at which to store output software images. Can be provided when zero or multiple Image IDs are provided. Cannot be provided with --vouch-for.

Optional Arguments:
  --image-finder IMAGE_FINDER
                        File path of Python script which implements image discovery interface. If not provided, script within Metabuild implementing image discovery interface will be auto-
                        discovered.
  --image-id IMAGE_ID [IMAGE_ID ...]
                        IDs of the images on which to operate. IDs of images to add as entries to Multi Image when performing --vouch-for operation. If not provided, all images in the Metabuild
                        identified by --chipset, --flavor, and --storage will be operated on.
  --chipset CHIPSET     Chipset whose images on which to operate. If not provided, images of all chipsets in the Metabuild will be operated on.
  --flavor FLAVOR       Chipset flavor whose images on which to operate. If not provided, images of all chipset flavors in the Metabuild will be operated on.
  --storage STORAGE     Chipset storage type whose images on which to operate. If not provided, images of all chipset storage types in the Metabuild will be operated on.
  --vouch-for           Defaults to false. If provided, --outfile will be a Multi Image and will contain the hashes of images identified by --image-id, --chipset, --flavor, and --storage.

For secure-image options: sectools metabuild-secure-image --secure-image-help
```

## sectools metabuild-secure-image --secure-image-help

```
Image Inputs:
  --fuse-blower-images FUSE_BLOWER_IMAGES [FUSE_BLOWER_IMAGES ...]
                        Fuse Blower Images (typically named sec.elf or sec.dat) whose fuse values will be cross checked against the image being validated when performing the --validate
                        operation.

Image Operations:
  --inspect             Print infile in a human-readable format.
  --verify-root VERIFY_ROOT
                        Root certificate hash to verify against the root certificate(s) of infile.
  --validate            If provided along with --outfile, validates --outfile against the --security-profile and any provided --fuse-blower-images. If --outfile is not provided, validates that
                        infile is compatible with the --security-profile and any provided --fuse-blower-images.
  --sign                Add or replace the signature and certificate chain of infile or newly generated Multi Image.
  --hash                Add or replace the Hash Table Segment of infile or newly generated Multi Image.
  --encrypt             Encrypt infile or newly generated Multi Image. If infile is already signed and hashing and signing is not being performed along with encryption, infile's preexisting
                        signature(s), certificate chain(s), and device restrictions will be persisted.

Image Format:
  --persist-sections    Retain all ELF sections of infile. If not provided, all ELF sections of infile will be removed. Must only be used when performing the --sign, --hash, or --encrypt
                        operations.
  --pil-split           PIL split --outfile. If not provided, --outfile will not be PIL split. Can only be used when performing the --sign, --hash, or --encrypt operations. The resulting PIL
                        split files will be saved in the same directory as --outfile if --pil-split-outdir is not provided. The name of the PIL split files will be prefixed with --outfile's
                        file name.
  --segment-hash-algorithm {SHA256,SHA384,SHA512}
                        Defaults to the algorithm specified in the --security-profile. Hash algorithm to use for computing Hash Table Segment hash entries when performing the --hash, --sign, or
                        --encrypt operations.

Authority:
  --qti                 Operate on infile or newly generated Multi Image as Qualcomm. If not provided, defaults to operating in OEM mode.

Signature Format:
  --signature-format SIGNATURE_FORMAT
                        Defaults to the signature format in --security-profile. Denotes the signature format to be used to sign --outfile. To list supported signature formats, provide
                        --available-signature-formats.

Signing Mode:
  --signing-mode {LOCAL,TEST,PLUGIN,CASS,QTI-REMOTE}
                        If LOCAL, locally provided signing keys and certificates are used to generate the signature and certificates. If TEST, Security Tools' prepackaged internal test signing
                        keys and certificates are used to generate the signature and certificates. If PLUGIN, generation of the signature and certificates is off-loaded to --plugin-signer. If
                        CASS, Qualcomm's Code Authorization Signing Service is used to generate the signature and certificates. If QTI-REMOTE, a Qualcomm proxy server is used to generate the
                        signature and certificates via CASS.

Local Signing (INSECURE):
  --outfile will contain a certificate chain of depth 3 when --ca-certificate is provided, else a certificate chain of depth 2. The leaf (Attestation) certificate will be created by the tool.

  --root-certificate ROOT_CERTIFICATE [ROOT_CERTIFICATE ...]
                        File path of one or more root certificates to use for signing.
  --root-key ROOT_KEY   File path of root key. Required if --ca-certificate is not provided.
  --ca-certificate CA_CERTIFICATE
                        File path of CA certificate to use for signing.
  --ca-key CA_KEY       File path of CA key. Required when --ca-certificate is provided.
  --attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT
                        Custom subject string to be included in the Attestation Certificate.

Test Signing (INSECURE):
  Test signing should never be used in production use cases. It is intended only for testing purposes. The private keys used for signing are contained within Security Tools and are available
  to anyone possessing Security Tools.

  --root-certificate-count {1,2,3,4}
                        Number of root certificates to use for signing. Defaults to 1.
  --attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT
                        Custom subject string to be included in the Attestation Certificate.

Plug-in Signing:
  --plugin-signer PLUGIN_SIGNER
                        File path of Python script which implements Plug-in Signer Interface.
  --plugin-signer-args PLUGIN_SIGNER_ARGS
                        Plug-in Signer implementation-specific inputs. --plugin-signer can implement handling of custom input parameters. Those parameters can be provided to --plugin-signer via
                        --plugin-signer-args.
  --attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT
                        Custom subject string to be included in the Attestation Certificate.

CASS Signing:
  --cass-password and --cass-password-file are mutually exclusive.

  --cass-capability CASS_CAPABILITY
                        CASS capability to use for signing. Provided by Qualcomm.
  --cass-password CASS_PASSWORD
                        CASS token password.
  --cass-password-file CASS_PASSWORD_FILE
                        File path of file containing CASS token password.
  --cass-token-serial-number CASS_TOKEN_SERIAL_NUMBER
                        Serial number of the CASS token. Used to identify the correct token when multiple are connected to the same machine. The serial number and additional token information
                        can be found in the SafeNet Authentication Client.

QTI Remote Signing:
  --cass-capability CASS_CAPABILITY
                        CASS capability to use for signing. Provided by Qualcomm.
  --qti-remote-signing-server-url QTI_REMOTE_SIGNING_SERVER_URL
                        URL of QTI Image Signing Server.
  --qti-remote-signing-server-port QTI_REMOTE_SIGNING_SERVER_PORT
                        Port of QTI Image Signing Server.

Root Key Type:
  --root-key-type {RTL-QTI,OTP-OEM,OTP-QTI}
                        Applicable only to UIE encryption. Defaults to the default_root_key_type in --security-profile. Identifies from where the device should retrieve the L1 decryption key
                        while decrypting --outfile.

Encryption Format:
  --encryption-format ENCRYPTION_FORMAT
                        Defaults to the encryption format in --security-profile. Denotes the encryption format to be used to encrypt --outfile. To list supported encryption formats, provide
                        --available-encryption-formats.

Encryption Mode:
  --encryption-mode {LOCAL,TEST,PLUGIN,QTI-REMOTE}
                        If LOCAL, locally provided encryption keys are used to generate the Encryption Parameters and encrypt --outfile. If TEST, Security Tools' prepackaged internal test
                        encryption keys are used to generate the Encryption Parameters and encrypt OUTFILE. If PLUGIN, generation of the Encryption Parameters is off-loaded to --plugin-
                        encrypter. If QTI-REMOTE, Qualcomm's Image Encryption Server is used to generate the Encryption Parameters.

Local UIE Encrypting (INSECURE):
  --l1-key L1_KEY       File path of L1 key to use for encrypting --l2-key.
  --l2-key L2_KEY       File path of L2 key to use for encrypting --l3-key. If not provided, a randomly generated key will be used.
  --l3-key L3_KEY       File path of L3 key to use for encrypting --outfile's loadable segments. If not provided, a randomly generated key will be used.

Local QBEC Encrypting:
  --data-encryption-key DATA_ENCRYPTION_KEY
                        File path of 256-bit key to use for QBEC XTS encrypting --outfile's encryptable segments. If not provided, a randomly generated key will be used.
  --device-public-key DEVICE_PUBLIC_KEY [DEVICE_PUBLIC_KEY ...]
                        File path of one or more device public keys to use to QBEC encrypt --outfile. Not applicable when operating as --qti.
  --encrypted-segment-index ENCRYPTED_SEGMENT_INDEX [ENCRYPTED_SEGMENT_INDEX ...]
                        Index and/or a range of indices of one or more segments in infile to be QBEC GCM encrypted. When providing a range, it must be of the form <lower_index>-<higher_index>.
                        If not provided, all LOAD segments will be encrypted.

Test Encrypting (INSECURE):
  Applicable only to UIE encryption. Test encryption should never be used in production use cases. It is intended only for testing purposes. The L1, L2, and L3 keys used for encryption are
  contained within Security Tools and are available to anyone possessing Security Tools. The symmetric L1 key's value is 0x6c26d6285ef322ef9ee58104b53496cb. The asymmetric L1 key's value is
  0x8cbd623695ab427530de8745e60d9137a796b5e6b63eb9ebea6e067dfe1addd8b1884298dd8cc3fcb7346accadbb0d9c897637f1fdbd2e05b2f89ce4ccc06f3b.

Plug-in Encrypting:
  Applicable only to UIE encryption.

  --plugin-encrypter PLUGIN_ENCRYPTER
                        File path of Python script which implements Plug-in Encrypter Interface.
  --plugin-encrypter-args PLUGIN_ENCRYPTER_ARGS
                        Plug-in Encrypter implementation-specific inputs. --plugin-encrypter can implement handling of custom input parameters. Those parameters can be provided to --plugin-
                        encrypter via --plugin-encrypter-args.

QTI Remote Encrypting:
  Applicable only to UIE encryption.

  --qti-remote-encryption-server-url QTI_REMOTE_ENCRYPTION_SERVER_URL
                        URL of QTI Image Encryption Server.
  --qti-remote-encryption-server-capability QTI_REMOTE_ENCRYPTION_SERVER_CAPABILITY
                        Capability to use for encrypting. Provided by Qualcomm.

Device Restrictions:
  --platform-binding {SOC-HW-VER,JTAG-ID,SOC-FEATURE-ID,PRODUCT-SEGMENT-ID,INDEPENDENT} [{SOC-HW-VER,JTAG-ID,SOC-FEATURE-ID,PRODUCT-SEGMENT-ID,INDEPENDENT} ...]
                        Chipset identifiers in --security-profile for which --outfile is authorized. If INDEPENDENT, --outfile is authorized for all devices irrespective of device SOC Hardware
                        Version, JTAG ID, SOC Feature ID, and Product Segment ID. SOC-FEATURE-ID and PRODUCT-SEGMENT-ID must be used with --qti.
  --variant VARIANT     Chipset variant for which --outfile is authorized. If not provided, --outfile is authorized for all chipset variants of the selected platform bindings.
  --serial-number SERIAL_NUMBER [SERIAL_NUMBER ...]
                        Serial number(s) of device(s) for which --outfile is authorized. If no serial numbers are provided, --outfile is authorized for all devices irrespective of device serial
                        number.
  --oem-id OEM_ID       OEM ID of devices for which --outfile is authorized. If no OEM ID is provided, --outfile is authorized for all devices irrespective of device OEM ID.
  --oem-product-id OEM_PRODUCT_ID
                        OEM Product ID of devices for which --outfile is authorized. If no OEM Product ID is provided, --outfile is authorized for all devices irrespective of device OEM Product
                        ID.
  --anti-rollback-version ANTI_ROLLBACK_VERSION
                        Anti-Rollback Version of --outfile. Defaults to 0. Once --outfile is loaded on a device, the device will fail to authenticate instances of --outfile which have Anti-
                        Rollback Versions lower than --anti-rollback-version.
  --root-certificate-index {0,1,2,3}
                        Defaults to 0. Specifies the index of the root certificate used to sign the next certificate in the certificate chain. Only applicable when --outfile is signed with
                        multiple root certificates.
  --transfer-root       Defaults to false. Enables revocation and activation of root certificates for devices to which --outfile is flashed. Only applicable when --outfile is signed with
                        multiple root certificates. Selection of root certificates to revoke and/or activate is achieved via mechanisms such as Devcfg.
  --measurement-register-target {HMR1,HMR2,FMR1,FMR2,FMR3,FMR4}
                        Measurement Register at which to store authentication measurement of --outfile. If no Measurement Register is provided, no measurement will be stored for --outfile.
  --oem-lifecycle-state {DEVELOPMENT,PRODUCTION}
                        OEM Lifecycle State of devices for which --outfile is authorized. If no OEM Lifecycle State is provided, --outfile is authorized for all devices irrespective of device
                        OEM Lifecycle State.
  --oem-root-certificate-hash OEM_ROOT_CERTIFICATE_HASH
                        OEM root certificate hash of devices for which --outfile is authorized. If no OEM root certificate hash is provided, --outfile is authorized for all devices irrespective
                        of device OEM root certificate hash. Must be used with --qti.
  --soc-lifecycle-state {RMA,OPERATIONAL-EXT,OPERATIONAL-INT} [{RMA,OPERATIONAL-EXT,OPERATIONAL-INT} ...]
                        SOC Lifecycle State of devices for which --outfile is authorized. If no SOC Lifecycle State is provided, --outfile is authorized for all devices irrespective of device
                        SOC Lifecycle State. Must be used with --qti.
  --jtag-debug {NOP,ENABLE,DISABLE}
                        Defaults to NOP. Determines whether the JTAG debug interface is re-enabled on devices to which --outfile is flashed. The specified action is taken after --outfile is
                        authenticated by the device. If NOP, there is no effect on the device's JTAG debug interface. If DISABLE, the device's JTAG debug interface is disabled. If ENABLE, the
                        device's JTAG debug interface is re-enabled unless it's been previously disabled.
  --secondary-software-id SECONDARY_SOFTWARE_ID
                        Secondary Software ID (also known as Trusted Application ID) of --outfile. Defaults to 0. Only applicable for Trusted Application images and is used by TrustZone to
                        distinguish Trusted Application images.
  --feature-id FEATURE_ID
                        Feature ID of --outfile. Only applicable for IP Protector images and is used by IP Protector to distinguish IP Protector images.
  --client-id CLIENT_ID
                        Client ID of --outfile. Only applicable for License Manager images and is used by License Manager to distinguish License Manager images.
  --library-id LIBRARY_ID
                        Library ID of --outfile. Only applicable for License Manager images and is used by License Manager to distinguish License Manager images.
  --transfer-uie-key    Defaults to false. Enables revocation and activation of Unified Image Encryption keys for devices to which --outfile is flashed. Selection of Unified Image Encryption
                        key to revoke and/or activate is achieved via mechanisms such as Devcfg.
  --crash-dump          Defaults to false. Enables complete system dumps on devices to which --outfile is flashed.
```

# sectools secure-debug

```
usage: sectools secure-debug [infile]
                             [-h] [-v] [--signing-help] [--available-signature-formats] [--available-device-restrictions] [--available-variants] [--outfile OUTFILE]
                             [--security-profile SECURITY_PROFILE] [--inspect] [--dump DUMP] [--verify-root VERIFY_ROOT] [--sign] [--hash] [--generate]
                             [--segment-hash-algorithm {SHA256,SHA384,SHA512}] [--qti] [--online-crash-dumps] [--offline-crash-dumps] [--logs] [--hlos-traces] [--adsp-hlos-traces]
                             [--modem-traces] [--all-traces] [--jtag-debug-hlos-traces] [--jtag-debug-adsp-hlos-traces] [--jtag-debug-modem] [--jtag-debug] [--nonsecure-crash-dumps]
                             [--apps-encrypted-mini-dumps] [--mpss-encrypted-mini-dumps] [--lpass-encrypted-mini-dumps] [--css-encrypted-mini-dumps] [--adsp-encrypted-mini-dumps]
                             [--cdsp-encrypted-mini-dumps] [--wlan-encrypted-mini-dumps] [--eud-uart] [--oem-flag-48] [--oem-flag-49] [--oem-flag-50] [--oem-flag-51] [--oem-flag-52]
                             [--oem-flag-53] [--oem-flag-54] [--oem-flag-55] [--oem-flag-56] [--oem-flag-57] [--oem-flag-58] [--oem-flag-59] [--oem-flag-60] [--oem-flag-61] [--oem-flag-62]
                             [--oem-flag-63] [--all-flags] [--qti-test-root-certificate-hash QTI_TEST_ROOT_CERTIFICATE_HASH [QTI_TEST_ROOT_CERTIFICATE_HASH ...]]
                             [--oem-test-root-certificate-hash OEM_TEST_ROOT_CERTIFICATE_HASH [OEM_TEST_ROOT_CERTIFICATE_HASH ...]] [--signature-format SIGNATURE_FORMAT]
                             [--signing-mode {LOCAL,TEST,PLUGIN,CASS,QTI-REMOTE}] [--root-certificate ROOT_CERTIFICATE [ROOT_CERTIFICATE ...]] [--root-key ROOT_KEY]
                             [--ca-certificate CA_CERTIFICATE] [--ca-key CA_KEY] [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT] [--root-certificate-count {1,2,3,4}]
                             [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT] [--plugin-signer PLUGIN_SIGNER] [--plugin-signer-args PLUGIN_SIGNER_ARGS]
                             [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT] [--cass-capability CASS_CAPABILITY] [--cass-password CASS_PASSWORD]
                             [--cass-password-file CASS_PASSWORD_FILE] [--cass-token-serial-number CASS_TOKEN_SERIAL_NUMBER] [--cass-capability CASS_CAPABILITY]
                             [--qti-remote-signing-server-url QTI_REMOTE_SIGNING_SERVER_URL] [--qti-remote-signing-server-port QTI_REMOTE_SIGNING_SERVER_PORT]
                             [--platform-binding {SOC-HW-VER,JTAG-ID,SOC-FEATURE-ID,PRODUCT-SEGMENT-ID,INDEPENDENT} [{SOC-HW-VER,JTAG-ID,SOC-FEATURE-ID,PRODUCT-SEGMENT-ID,INDEPENDENT} ...]]
                             [--variant VARIANT] [--serial-number SERIAL_NUMBER [SERIAL_NUMBER ...]] [--oem-id OEM_ID] [--oem-product-id OEM_PRODUCT_ID]
                             [--anti-rollback-version ANTI_ROLLBACK_VERSION] [--root-certificate-index {0,1,2,3}] [--transfer-root]
                             [--measurement-register-target {HMR1,HMR2,FMR1,FMR2,FMR3,FMR4}] [--oem-lifecycle-state {DEVELOPMENT,PRODUCTION}]
                             [--soc-lifecycle-state {RMA,OPERATIONAL-EXT,OPERATIONAL-INT} [{RMA,OPERATIONAL-EXT,OPERATIONAL-INT} ...]]

Tool for generating and signing Debug Policy images enabling device debugging and authentication.

Help:
  -h, --help            Show this help message and exit. Debug Policy Secure Flags, Debug Policy Non-Secure Flags, Authority, and Root Certificate Hash command-line arguments are generated
                        dynamically based on the Security Profile. Provide --help and --security-profile to see all the available options.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.
  --signing-help        Show signing options and exit.
  --available-signature-formats
                        Show available --signature-format values and exit. Must be used with --security-profile.
  --available-device-restrictions
                        Show available device restrictions when performing the --sign or --hash operations.
  --available-variants  Show available --variant values and exit. Must be used with --security-profile.

Image Inputs:
  infile                File path of input software image.

Image Outputs:
  --outfile OUTFILE     File path of output software image.

Security Profile:
  --security-profile SECURITY_PROFILE
                        File path of a Security Profile XML. A Security Profile describes the security features of a Qualcomm chipset.

Image Operations:
  --inspect             Print infile in a human-readable format.
  --dump DUMP           Decompose infile and store its regions at the specified directory.
  --verify-root VERIFY_ROOT
                        Root certificate hash to verify against the root certificate(s) of infile.
  --sign                Add or replace the signature and certificate chain of infile or newly generated Debug Policy image.
  --hash                Add or replace the Hash Table Segment of infile or newly generated Debug Policy image.
  --generate            Generate a new Debug Policy image.

Image Format:
  --segment-hash-algorithm {SHA256,SHA384,SHA512}
                        Defaults to the algorithm specified in the --security-profile. Hash algorithm to use for computing Hash Table Segment hash entries when performing the --hash or --sign
                        operations.

Authority:
  Authority command-line argument is generated dynamically based on the Security Profile. Provide --help and --security-profile to see if it is available.

  --qti                 Operate on infile or newly generated Debug Policy image as Qualcomm. If not provided, defaults to operating in OEM mode.

Debug Policy Secure Flags:
  Must provide --serial-number when generating a Debug Policy image using these options. Debug Policy Secure Flags command-line arguments are generated dynamically based on the Security
  Profile. Provide --help and --security-profile to see all the available options.

  --online-crash-dumps  Specific to Windows devices. Enable RAM dumps after device has booted to HLOS. Dumps can be collected regardless of whether device resets.
  --offline-crash-dumps
                        Enable RAM dumps. Dumps can only be collected after device resets.
  --logs                Enable QTEE and Trusted Application logging.
  --hlos-traces         Enable traces for HLOS.
  --adsp-hlos-traces    Enable traces for ADSP and HLOS.
  --modem-traces        Enable traces for Modem Subsystem.
  --all-traces          Enable traces for QTEE, ADSP, and HLOS.
  --jtag-debug-hlos-traces
                        Enable JTAG debugging and traces for HLOS.
  --jtag-debug-adsp-hlos-traces
                        Enable JTAG debugging and traces for ADSP and HLOS.
  --jtag-debug-modem    Enable JTAG debugging and traces for Modem subsystem.
  --jtag-debug          Enable JTAG debugging and traces for all subsystems.

Debug Policy Non-Secure Flags:
  Debug Policy Non-Secure Flags command-line arguments are generated dynamically based on the Security Profile. Provide --help and --security-profile to see all the available options.

  --nonsecure-crash-dumps
                        Enable crash dumps of memory other than QTEE/QSEE secure regions. QTEE Diag log region is encrypted.
  --apps-encrypted-mini-dumps
                        Enable encrypted mini dumps for APPS.
  --mpss-encrypted-mini-dumps
                        Enable encrypted mini dumps for MPPS.
  --lpass-encrypted-mini-dumps
                        Enable encrypted mini dumps for LPASS.
  --css-encrypted-mini-dumps
                        Enable encrypted mini dumps for CSS.
  --adsp-encrypted-mini-dumps
                        Enable encrypted mini dumps for ADSP.
  --cdsp-encrypted-mini-dumps
                        Enable encrypted mini dumps for CDSP.
  --wlan-encrypted-mini-dumps
                        Enable encrypted mini dumps for WLAN.
  --eud-uart            Enable EUD UART debugging.

OEM-Designated Flags:
  Flags for which the OEM defines the meaning.

  --oem-flag-48         Set the debug flag at bit 48.
  --oem-flag-49         Set the debug flag at bit 49.
  --oem-flag-50         Set the debug flag at bit 50.
  --oem-flag-51         Set the debug flag at bit 51.
  --oem-flag-52         Set the debug flag at bit 52.
  --oem-flag-53         Set the debug flag at bit 53.
  --oem-flag-54         Set the debug flag at bit 54.
  --oem-flag-55         Set the debug flag at bit 55.
  --oem-flag-56         Set the debug flag at bit 56.
  --oem-flag-57         Set the debug flag at bit 57.
  --oem-flag-58         Set the debug flag at bit 58.
  --oem-flag-59         Set the debug flag at bit 59.
  --oem-flag-60         Set the debug flag at bit 60.
  --oem-flag-61         Set the debug flag at bit 61.
  --oem-flag-62         Set the debug flag at bit 62.
  --oem-flag-63         Set the debug flag at bit 63.

Enable All Debug Policy Flags:
  Does not enable OEM-designated flags. To enable OEM-designated flags, you must specifically provide the arguments in the OEM-Designated Flags Group.

  --all-flags           Enable all Debug Policy flags.

Root Certificate Hash:
  Root Certificate Hash command-line arguments are generated dynamically based on the Security Profile. Provide --help and --security-profile to see all the available options.

  --qti-test-root-certificate-hash QTI_TEST_ROOT_CERTIFICATE_HASH [QTI_TEST_ROOT_CERTIFICATE_HASH ...]
                        Specify up to 4 SHA256 or SHA384 QTI root certificate hash strings. They provide alternative roots of trust when authenticating QTI-signed images. It must be used with
                        the --qti option.
  --oem-test-root-certificate-hash OEM_TEST_ROOT_CERTIFICATE_HASH [OEM_TEST_ROOT_CERTIFICATE_HASH ...]
                        Specify up to 4 SHA256 or SHA384 OEM root certificate hash strings. They provide alternative roots of trust when authenticating OEM-signed images.

Debug Policy Secure Flags, Debug Policy Non-Secure Flags, Authority, and Root Certificate Hash command-line arguments are generated dynamically based on the Security Profile. Provide --help and
--security-profile to see all the available options.
```

# sectools tme-secure-debug

```
usage: sectools tme-secure-debug [infile]
                                 [-h] [-v] [--available-variants] [--available-device-restrictions] [--signing-help] [--available-signature-formats] [--dec DEC] [--qti-dpr QTI_DPR]
                                 [--slc SLC [SLC ...]] [--outfile OUTFILE] [--security-profile SECURITY_PROFILE] [--inspect] [--dump DUMP] [--sign] [--hash] [--generate]
                                 [--verify-root VERIFY_ROOT] [--segment-hash-algorithm {SHA256,SHA384,SHA512}] [--qti] [--enable-test-signed ENABLE_TEST_SIGNED [ENABLE_TEST_SIGNED ...]]
                                 [--oem-test-root-certificate-hash OEM_TEST_ROOT_CERTIFICATE_HASH [OEM_TEST_ROOT_CERTIFICATE_HASH ...]] [--oem-crash-dump-public-key OEM_CRASH_DUMP_PUBLIC_KEY]
                                 [--persist-on-reset] [--disable-system-watchdog] [--allow-system-watchdog-access]
                                 [--crash-dump {MINI_DUMP,NS_FULL_DUMP,SEC_FULL_DUMP} [{MINI_DUMP,NS_FULL_DUMP,SEC_FULL_DUMP} ...]] [--oem-id OEM_ID] [--oem-product-id OEM_PRODUCT_ID]
                                 [--soc-lifecycle-state {OPERATIONAL-EXT,RMA,OPERATIONAL-INT}] [--platform-binding {SOC-FEATURE-ID,SOC-HW-VER,JTAG-ID} [{SOC-FEATURE-ID,SOC-HW-VER,JTAG-ID} ...]]
                                 [--variant VARIANT] [--serial-number SERIAL_NUMBER [SERIAL_NUMBER ...]] [--oem-root-certificate-hash OEM_ROOT_CERTIFICATE_HASH]
                                 [--oem-lifecycle-state {PRODUCTION,DEVELOPMENT}] [--oem-batch-key-hash OEM_BATCH_KEY_HASH] [--anti-rollback-version ANTI_ROLLBACK_VERSION]
                                 [--root-certificate-index {0,1,2,3}] [--transfer-root] [--measurement-register-target {HMR1,HMR2,FMR1,FMR2,FMR3,FMR4}] [--signature-format SIGNATURE_FORMAT]
                                 [--signing-mode {LOCAL,TEST,PLUGIN,CASS}] [--root-key ROOT_KEY] [--root-certificate ROOT_CERTIFICATE [ROOT_CERTIFICATE ...]] [--ca-certificate CA_CERTIFICATE]
                                 [--ca-key CA_KEY] [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT] [--root-certificate-count {1,2,3,4}]
                                 [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT] [--plugin-signer PLUGIN_SIGNER] [--plugin-signer-args PLUGIN_SIGNER_ARGS]
                                 [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT] [--cass-capability CASS_CAPABILITY] [--cass-password CASS_PASSWORD]
                                 [--cass-password-file CASS_PASSWORD_FILE] [--cass-token-serial-number CASS_TOKEN_SERIAL_NUMBER]

Tool for generating and signing TME Debug Policy images enabling device debugging and authentication.

Help:
  -h, --help            Show this help message and exit. Some command-line arguments are generated dynamically based on the Security Profile. Provide --help and --security-profile to see all
                        the available options.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.
  --available-variants  Show available --variant values and exit. Must be used with --security-profile.
  --available-device-restrictions
                        Show available device restrictions when performing the --sign or --hash operations.
  --signing-help        Show signing options and exit.
  --available-signature-formats
                        Show available --signature-format values and exit. Must be used with --security-profile.

Image Inputs:
  infile                File path of input software image.
  --dec DEC             File path of Debug Entitlement Certificate (DEC) to use for TME Debug Policy generation. If creating multiple TME Debug Policies, a separate DEC must be provided for
                        each TME Debug Policy being created.
  --qti-dpr QTI_DPR     File path of a QTI Debug Policy Request (DPR) to be packaged within OEM Debug Policy ELF. Can only be used during OEM Debug Policy generation. Cannot be used with --qti.
  --slc SLC [SLC ...]   File path of one or more Service Layer Commands (SLC) to be packaged within OEM Debug Policy ELF. Can only be used during OEM Debug Policy generation. Cannot be used
                        with --qti.

Image Outputs:
  --outfile OUTFILE     File path of output software image.

Security Profile:
  --security-profile SECURITY_PROFILE
                        File path of a Security Profile XML. A Security Profile describes the security features of a Qualcomm chipset.

Image Operations:
  --inspect             Print infile in a human-readable format.
  --dump DUMP           Decompose infile and store its regions at the specified directory.
  --sign                Add or replace the signature of infile or newly generated TME Debug Policy image. Also add or replace the certificate chain of infile or newly generated TME Debug Policy
                        image if signing an OEM Debug Policy ELF.
  --hash                Add or replace the Hash Table Segment of infile or newly generated OEM Debug Policy ELF. Cannot be used with --qti.
  --generate            Generate a new TME Debug Policy image. A QTI Debug Policy Request (DPR) binary will be generated if operating in QTI mode. When operating in OEM mode, an OEM Debug
                        Policy ELF or OEM DPR will be generated depending on the Security Profile. If generating an OEM Debug Policy ELF, multiple OEM DPRs can be generated at once by
                        clustering the arguments of each desired DPR via --new-dpr. For example: sectools tme-secure-debug <first OEM DPR args> --new-dpr <second OEM DPR args> ...
  --verify-root VERIFY_ROOT
                        Root certificate hash to verify against the root certificate(s) of infile. Only applicable for an OEM Debug Policy ELF.

Image Format:
  --segment-hash-algorithm {SHA256,SHA384,SHA512}
                        Defaults to the algorithm specified in the --security-profile. Hash algorithm to use for computing Hash Table Segment hash entries when performing the --hash or --sign
                        operations. Only applicable for an OEM Debug Policy ELF.

Authority:
  --qti                 Operate on infile or newly generated TME Debug Policy image as Qualcomm. If not provided, defaults to operating in OEM mode.

QTI Test Signed Images:
  All options must be used with --qti. Some QTI test signing command-line arguments are generated dynamically based on the Security Profile. Provide --help and --security-profile to see all
  the available options.

  --enable-test-signed ENABLE_TEST_SIGNED [ENABLE_TEST_SIGNED ...]
                        File path of one or more QTI test-signed binaries for which to enable authentication. Binaries can be ELF with v7 Hash Table Segment or Image Authentication Request
                        (IAR).

OEM Test Signed Images:
  --oem-test-root-certificate-hash OEM_TEST_ROOT_CERTIFICATE_HASH [OEM_TEST_ROOT_CERTIFICATE_HASH ...]
                        Specify one or more SHA384 or SHA512 OEM root certificate hash strings. They provide alternative roots of trust when authenticating OEM-signed images. The maximum number
                        of supported hashes depends on the Security Profile.

Debug Options:
  Additional debug and subsystem-specific debug command-line arguments are generated dynamically based on the Security Profile. Provide --help and --security-profile to see all the available
  options.

  --oem-crash-dump-public-key OEM_CRASH_DUMP_PUBLIC_KEY
                        File path of public key used to encrypt crash dumps.
  --persist-on-reset    Allows debug policy updates to the debug vector to persist on soft reset. This option helps JTAG enablement in APPS or TME subsystem as early as the first line of Boot
                        ROM code.
  --disable-system-watchdog
                        Disables the system watchdog for global STOP_ON_FAIL support.
  --allow-system-watchdog-access
                        Allows the APPS Secure and AOP subsystems to access system watchdog registers for selective STOP_ON_FAIL support.
  --crash-dump {MINI_DUMP,NS_FULL_DUMP,SEC_FULL_DUMP} [{MINI_DUMP,NS_FULL_DUMP,SEC_FULL_DUMP} ...]
                        Used in conjunction with Debug Options to enable crash dump for a specific subsystem.

Some command-line arguments are generated dynamically based on the Security Profile. Provide --help and --security-profile to see all the available options.
```

# sectools fuse-blower

```
usage: sectools fuse-blower [infile]
                            [-h] [-v] [--signing-help] [--available-variants] [--available-signature-formats] [--available-device-restrictions] [--available-fuse-groups]
                            [--show-recommended-fuses] [--show-oem-choice-fuses] [--outfile OUTFILE] [--security-profile SECURITY_PROFILE] [--inspect] [--dump DUMP] [--verify-root VERIFY_ROOT]
                            [--sign] [--hash] [--generate] [--segment-hash-algorithm {SHA256,SHA384,SHA512}] [--signature-format SIGNATURE_FORMAT] [--signing-mode {LOCAL,TEST,PLUGIN,CASS}]
                            [--root-certificate ROOT_CERTIFICATE [ROOT_CERTIFICATE ...]] [--root-key ROOT_KEY] [--ca-certificate CA_CERTIFICATE] [--ca-key CA_KEY]
                            [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT] [--root-certificate-count {1,2,3,4}] [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT]
                            [--plugin-signer PLUGIN_SIGNER] [--plugin-signer-args PLUGIN_SIGNER_ARGS] [--attest-certificate-subject ATTEST_CERTIFICATE_SUBJECT]
                            [--cass-capability CASS_CAPABILITY] [--cass-password CASS_PASSWORD] [--cass-password-file CASS_PASSWORD_FILE] [--cass-token-serial-number CASS_TOKEN_SERIAL_NUMBER]
                            [--platform-binding {SOC-HW-VER,JTAG-ID,INDEPENDENT} [{SOC-HW-VER,JTAG-ID,INDEPENDENT} ...]] [--variant VARIANT] [--serial-number SERIAL_NUMBER [SERIAL_NUMBER ...]]
                            [--oem-id OEM_ID] [--oem-product-id OEM_PRODUCT_ID] [--anti-rollback-version ANTI_ROLLBACK_VERSION] [--root-certificate-index {0,1,2,3}] [--transfer-root]
                            [--measurement-register-target {HMR1,HMR2,FMR1,FMR2,FMR3,FMR4}] [--oem-lifecycle-state {DEVELOPMENT,PRODUCTION}]

Tool for generating and signing Fuse Blower images. When consumed by a device, a Fuse Blower image results in specified fuses being blown.

Help:
  -h, --help            Show this help message and exit. Fuse, Fuse Groups, and Recommended Fuses command-line arguments are generated dynamically based on the Security Profile. Provide --help
                        and --security-profile to see all the available options. Refer to the chipset-specific QFPROM Programming Reference Guide for further information on fuses.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.
  --signing-help        Show signing options and exit.
  --available-variants  Show available --variant values and exit. Must be used with --security-profile.
  --available-signature-formats
                        Show available --signature-format values and exit. Must be used with --security-profile.
  --available-device-restrictions
                        Show available device restrictions when performing the --sign or --hash operations.
  --available-fuse-groups
                        Show available --fuse-group values, as well as the equivalent fuse arguments for each group. Must be used with --security-profile.
  --show-recommended-fuses
                        Show a list of fuse arguments equivalent to the fuses set via --recommended-fuses. Fuse arguments marked "OEM Value" require an OEM-chosen value. Must be used with
                        --security-profile.
  --show-oem-choice-fuses
                        Show a list of fuse arguments for which there is no Qualcomm recommendation and can be set at the OEM's discretion. Must be used with --security-profile.

Image Inputs:
  infile                File path of input software image.

Image Outputs:
  --outfile OUTFILE     File path of output software image.

Security Profile:
  --security-profile SECURITY_PROFILE
                        File path of a Security Profile XML. A Security Profile describes the security features of a Qualcomm chipset.

Image Operations:
  --inspect             Print infile in a human-readable format. Provide --security-profile to see additional information for non-zero fuse values when inspecting a Fuse Blower image.
  --dump DUMP           Decompose infile and store its regions at the specified directory.
  --verify-root VERIFY_ROOT
                        Root certificate hash to verify against the root certificate(s) of infile. Only applicable when operating on an ELF Fuse Blower image (typically named sec.elf).
  --sign                Add or replace the signature and certificate chain of infile or newly generated Fuse Blower image. Only applicable when operating on an ELF Fuse Blower image (typically
                        named sec.elf).
  --hash                Add or replace the Hash Table Segment of infile or newly generated Fuse Blower image. Only applicable when operating on an ELF Fuse Blower image (typically named
                        sec.elf).
  --generate            Generate a new Fuse Blower image. To blow random values to a fuse row address, specify <fuse_name>=RANDOM when performing the --generate operation.

Image Format:
  --segment-hash-algorithm {SHA256,SHA384,SHA512}
                        Defaults to the algorithm specified in the --security-profile. Hash algorithm to use for computing Hash Table Segment hash entries when performing the --hash or --sign
                        operations. Only applicable when operating on an ELF Fuse Blower image (typically named sec.elf).

Fuse, Fuse Groups, and Recommended Fuses command-line arguments are generated dynamically based on the Security Profile. Provide --help and --security-profile to see all the available options.
Refer to the chipset-specific QFPROM Programming Reference Guide for further information on fuses. To blow random values to a fuse row address, specify <fuse_name>=RANDOM when performing the
--generate operation.
```

# sectools fuse-validator

```
usage: sectools fuse-validator [-h] operation ...

Tool for validating a device's blown fuses. Payload requests generated via 'generate-payload' are formatted for either on-target or off-target comparison. Devices respond to a payload request
with a payload response of the same type. Off-target payload responses are compared via 'compare'. On-target payloads are displayed via 'show-on-target-results'.

Help:
  -h, --help  Show this help message and exit.

Required Arguments:
  operation   generate-payload, compare, or show-on-target-results

For help menu of a specific operation: sectools fuse-validator <operation> -h
```

# sectools elf-tool

```
usage: sectools elf-tool [-h] operation ...

Tool for generating, adding segments to, removing sections from, and combining ELF software images.

Help:
  -h, --help  Show this help message and exit.

Required Arguments:
  operation   generate, insert, remove-sections, or combine

For help menu of a specific operation: sectools elf-tool <operation> -h
```

## sectools elf-tool generate

```
usage: sectools elf-tool generate [-h] [-v] [--available-elf-machine-types] [--data DATA] [--outfile OUTFILE] [--elf-class {32,64}] [--elf-entry ELF_ENTRY] [--elf-machine-type ELF_MACHINE_TYPE]
                                  [--type {NULL,LOAD,NOTE}] [--offset OFFSET] [--vaddr VADDR] [--paddr PADDR] [--memsz MEMSZ] [--flags FLAGS] [--align ALIGN]

Generate a new ELF software image containing a segment as specified via Segment Configuration arguments.

Help:
  -h, --help            Show this help message and exit.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.
  --available-elf-machine-types
                        Show available --elf-machine-type values and exit.

Image Inputs:
  --data DATA           File path of segment data.

Image Outputs:
  --outfile OUTFILE     File path of output ELF image.

ELF Configuration:
  --elf-class {32,64}   Defaults to 64.
  --elf-entry ELF_ENTRY
                        Entry point address. Defaults to 0x0.
  --elf-machine-type ELF_MACHINE_TYPE
                        Architecture of output ELF image. Defaults to ARM (ARM 32-bit architecture (AARCH32)). Provide --available-elf-machine-types for available values.

Segment Configuration:
  Program Header values of segment containing --data.

  --type {NULL,LOAD,NOTE}
                        Defaults to LOAD.
  --offset OFFSET       Defaults to the lowest available offset following the ELF Header and Program Header Table.
  --vaddr VADDR         Defaults to 0x0.
  --paddr PADDR         Defaults to 0x0.
  --memsz MEMSZ         Defaults to size of --data.
  --flags FLAGS         Defaults to 0x0.
  --align ALIGN         Defaults to 0x0.
```

## sectools elf-tool insert

```
usage: sectools elf-tool insert infile
                                [-h] [-v] --data DATA --outfile OUTFILE [--type {NULL,LOAD,NOTE}] [--offset OFFSET] [--vaddr VADDR] [--paddr PADDR] [--memsz MEMSZ] [--flags FLAGS]
                                [--align ALIGN]

Add a segment specified via Segment Configuration arguments to an existing ELF software image.

Help:
  -h, --help            Show this help message and exit.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.

Image Inputs:
  infile                File path of input ELF image.
  --data DATA           File path of segment data.

Image Outputs:
  --outfile OUTFILE     File path of output ELF image.

Segment Configuration:
  Program Header values of segment containing --data.

  --type {NULL,LOAD,NOTE}
                        Defaults to LOAD.
  --offset OFFSET       Defaults to the lowest available offset following the ELF Header, Program Header Table, and existing segments. If infile's ELF Header, Program Header Table, Section
                        Header Table, existing segments, or existing sections overlap --offset, the next available offset will be used.
  --vaddr VADDR         Defaults to 0x0.
  --paddr PADDR         Defaults to 0x0.
  --memsz MEMSZ         Defaults to size of --data.
  --flags FLAGS         Defaults to 0x0.
  --align ALIGN         Defaults to 0x0.
```

## sectools elf-tool remove-sections

```
usage: sectools elf-tool remove-sections [-h] [-v] --outfile OUTFILE infile

Remove Sections from an existing ELF software image.

Help:
  -h, --help         Show this help message and exit.
  -v, --verbose      Enable verbose logging. Repeat for increased verbosity.

Image Inputs:
  infile             File path of input ELF image.

Image Outputs:
  --outfile OUTFILE  File path of output ELF image.
```

## sectools elf-tool combine

```
usage: sectools elf-tool combine [-h] [-v] --outfile OUTFILE [--elf-entry ELF_ENTRY] infile [infile ...]

Combine multiple ELFs into a single ELF. Data contained within ELF sections will not be persisted unless they are encapsulated within segments.

Help:
  -h, --help            Show this help message and exit.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.

Image Inputs:
  infile                File path of input ELF images.

Image Outputs:
  --outfile OUTFILE     File path of output ELF image.

ELF Configuration:
  --elf-entry ELF_ENTRY
                        Entry point address. Defaults to entry point address of first infile.
```

# sectools elf-consolidator

```
usage: sectools elf-consolidator [-h] [-v] [--images IMAGES [IMAGES ...]] [--qti-dpr QTI_DPR] [--config CONFIG] [--outfile OUTFILE] [--pil-split] [--pil-split-outdir PIL_SPLIT_OUTDIR]

Tool for generating Consolidated ELF software images. A Consolidated ELF contains the contents of multiple subsystem images.

Help:
  -h, --help            Show this help message and exit.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.

Image Inputs:
  --images IMAGES [IMAGES ...]
                        Input ELF images to be added to the Consolidated ELF.
  --qti-dpr QTI_DPR     Debug Policy Request (DPR) to be added to the Consolidated ELF.
  --config CONFIG       The configuration file that describes the Consolidated ELF format of a Qualcomm chipset.

Image Outputs:
  --outfile OUTFILE     File path of output Consolidated ELF image.

Image Format:
  --pil-split           PIL split --outfile. If not provided, --outfile will not be PIL split. The resulting PIL split files will be saved in the same directory as --outfile if --pil-split-
                        outdir is not provided. The name of the PIL split files will be prefixed with --outfile's file name.
  --pil-split-outdir PIL_SPLIT_OUTDIR
                        Directory at which to store PIL split files. Must be used with --pil-split.
```

# sectools mbn-tool

```
usage: sectools mbn-tool [-h] operation ...

Tool to prepend an MBN Header to a binary image.

Help:
  -h, --help  Show this help message and exit.

Required Arguments:
  operation   generate

For help menu of a specific operation: sectools mbn-tool <operation> -h
```

## sectools mbn-tool generate

```
usage: sectools mbn-tool generate [-h] [-v] --data DATA --outfile OUTFILE --mbn-version {3,5,6,7}

Prepend an MBN Header to a binary image.

Help:
  -h, --help            Show this help message and exit.
  -v, --verbose         Enable verbose logging. Repeat for increased verbosity.

Required Arguments:
  --data DATA           File path of data to prepend with an MBN Header.
  --outfile OUTFILE     File path of output MBN.
  --mbn-version {3,5,6,7}
                        Version of MBN Header to prepend to --data.
```
