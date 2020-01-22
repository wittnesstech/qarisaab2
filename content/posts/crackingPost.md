# Breaking Office 2013's Locks

---

## Homework

- [x] Made a test file
- [x] Got the hash from [online hash extractor][onlinehashurl]

`$office$*2013*100000*256*16*08e512c7771fb0c97c3fca5dcae58ea3*e73812186296dac13fc627ea84a86bca*c0f6f63de3be4c9fbacfff43001c980f0945cabfa757a2b96751f9da1c896103`

- [x] Researched for details of [Office Encryption][officeencryptionhistory]

| Office Version | Encryption                 | Technique                                                                                                                        |
| -------------- | -------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `Office 2007`  | 128-bit **[AES][aeswiki]** | The password is stretched into a 128-bit AES key 50,000 times using SHA-1 hash function                                          |
| `Office 2010`  | 128-bit **[AES][aeswiki]** | Number of SHA-1 conversions has doubled to 100,000                                                                               |
| `Office 2013`  | 128-bit **[AES][aeswiki]** | Uses 128-bit [AES][aeswiki], again with hash algorithm SHA-1                                                                     |
| `Office 2016`  | **256-bit [AES][aeswiki]** | Uses [Cipher Block Chaining](<https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_Block_Chaining_(CBC)>>>>>>>>>) |

- [x] Locate Hash identifiers

| Hash-Mode (-m) | Hash-Name      | Example (--username)                                                                                                                                             |
| -------------- | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 9400           | `Office 2007`  | `$office$*2007*20*128*16*411a51284e0d0200b131a8949aaaa5cc*117d532441c63968bee7647d9b7df7d6*df1d601ccf905b375575108f42ef838fb88e1cde`                             |
| 9500           | `Office 2010`  | `$office$*2010*100000*128*16*77233201017277788267221014757262*b2d0ca4854ba19cf95a2647d5eee906c*e30cbbb189575cafb6f142a90c2622fa9e78d293c5b0c001517b3f5b82993557` |
| 9600           | `Office 2013`  | `$office$*2013*100000*256*16*7dd611d7eb4c899f74816d1dec817b3b*948dc0b2c2c6c32f14b5995a543ad037*0b7ee0e48e935f937192a59de48a7d561ef2691d5c8a3ba87ec2d04402a94895` |
| 9710           | `Office 97-03` | `$oldoffice$1*04477077758555626246182730342136*b1b72ff351e41a7c68f6b45c4e938bd6*0d95331895e99f73ef8b6fbc4a78ac1a` (MD5+RC4, collider-mode#1)                     |
| 9720           | `Office 97-03` | `$oldoffice$1*04477077758555626246182730342136*b1b72ff351e41a7c68f6b45c4e938bd6*0d95331895e99f73ef8b6fbc4a78ac1a` (MD5+RC4, collider-mode#2)                     |

### Executing [HashCat]

`echo \$office\$*2013*100000*256*16*...*...*... > hash2013`

`hashcat -m 9600 -o cracked2013 hash2013 rockyou.txt`

#### Final Output

`cat cracked2013`

> $office$_2013_100000_256_16_...\_...\*...:**password**

[aeswiki]: https://en.wikipedia.org/wiki/Advanced_Encryption_Standard
[hashcat]: https://hashcat.net/hashcat/
[officeencryptionhistory]: https://en.wikipedia.org/wiki/Microsoft_Office_password_protection#History_of_Microsoft_Encryption_password
[onlinehashurl]: https://www.onlinehashcrack.com/tools-office-hash-extractor.php
