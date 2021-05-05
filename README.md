# Kotlin-extensions
A collection of useful Kotlin extension functions in one place.

### Extensions
* [Views](#views)
* [Contexts](#contexts)
  * [Activity](#activity)
  * [Fragments](#fragments)
  * [Application](#application)
* [Security](#security)
* [Dialogs](#dialogs)


## Views

## Contexts

### Activity

### Fragments

### Application

## Security
```kotlin
/**
 * Extension method to make easy encryption/decryption for any string using AES .
 */
import android.util.Base64
import javax.crypto.Cipher
import javax.crypto.spec.IvParameterSpec
import javax.crypto.spec.SecretKeySpec

// TODO replace with you secret key
private const val SECRET_KEY = "23623@smdhsdhsjd"

private val byteIV: ByteArray = byteArrayOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16)

private fun String.encrypt(): String? {
    return try {
        val cipher = Cipher.getInstance("AES/CBC/ZeroBytePadding")
        cipher.init(
            Cipher.ENCRYPT_MODE,
            SecretKeySpec(SECRET_KEY.toByteArray(charset("UTF-8")), "AES"),
            IvParameterSpec(byteIV)
        )
        val bytes = cipher.doFinal(this.toByteArray(charset("UTF-8")))
        Base64.encodeToString(bytes, Base64.NO_WRAP)
    } catch (ex: Exception) {
        null
    }
}

private fun String.decrypt(): String? {
    return try {
        val cipher = Cipher.getInstance("AES/CBC/ZeroBytePadding")
        cipher.init(
            Cipher.DECRYPT_MODE,
            SecretKeySpec(SECRET_KEY.toByteArray(charset("UTF-8")), "AES"),
            IvParameterSpec(byteIV)
        )
        String(cipher.doFinal(Base64.decode(this, Base64.NO_WRAP)))
    } catch (ex: Exception) {
        null
    }
}
```

## Dialogs
