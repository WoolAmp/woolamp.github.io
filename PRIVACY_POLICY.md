# WoolAmp Privacy Policy

**Effective date:** September 24, 2026

WoolAmp is an Android music player. This Privacy Policy explains what information WoolAmp processes, when information leaves your device, and the choices available to you.

WoolAmp is designed as a local-first music player. Most playback, library, DSP, equalizer, headphone-correction, preset, skin, playlist, and preference processing happens on your Android device.

## 1. Local music and media access

WoolAmp asks Android for access to audio media so it can discover and play music available to the app. It may read information associated with those files, including title, artist, album, duration, file or content identifiers, embedded artwork, and other music metadata.

Reading or playing a local audio file does not mean WoolAmp uploads that file. WoolAmp does not upload the audio content of your local music files to its entitlement service or to metadata/lyrics providers as part of the features described below.

## 2. On-device audio processing

WoolAmp's real-time playback and DSP processing—including equalization, headphone correction, crossfeed, spatial processing, ReplayGain-related local analysis, and other audio processing—runs on your device.

Local ReplayGain/audio analysis remains available even when optional online metadata enrichment is disabled.

## 3. Online Metadata & Lyrics — optional and off by default

**Online Metadata & Lyrics is OFF by default.** WoolAmp does not perform unattended online enrichment of your local library unless you affirmatively enable this feature in **Settings → Privacy & Network Services**.

Before enabling it, WoolAmp explains that online services may receive information from your music library. If you enable the feature, WoolAmp may send information needed for a lookup, such as:

- artist name;
- track title;
- album title;
- track duration;
- ISRC;
- MusicBrainz recording, release, or release-group identifiers; and
- similar music identifiers already associated with the track.

Depending on the lookup and the release configuration, WoolAmp can use services including:

- LRCLIB for lyrics;
- Wikidata and Wikimedia Commons for structured music/artist information and eligible artwork;
- AcousticBrainz for recording-related audio-feature metadata; and
- MusicBrainz and Cover Art Archive when hosted MusicBrainz enrichment is enabled for that release.

These providers receive ordinary connection information such as your IP address when your device connects to them. Their handling of information is governed by their own policies.

Your audio files are not uploaded for these enrichment lookups.

You can turn Online Metadata & Lyrics off at any time. Turning it off cancels queued automatic online enrichment work but does not automatically delete metadata or artwork already downloaded. WoolAmp also provides a **Clear Cached Online Data** action for provider-response and downloaded artist-presentation caches.

## 4. Internet Radio

Internet Radio is an explicit network feature. WoolAmp can contact the Radio Browser directory when you browse or search for stations. Search text, filters, and ordinary network information may therefore be sent to that directory.

When you choose a station, your device connects directly to the selected station or its streaming/CDN provider. That provider can receive normal connection information such as your IP address, user-agent information, and stream requests. WoolAmp does not operate those independent stations.

## 5. Music Locker and user-configured servers

WoolAmp can connect to supported self-hosted music servers that you configure. The current beta implementation includes an OpenSubsonic-compatible Music Locker connector.

Release builds require **HTTPS** Music Locker server URLs. WoolAmp does not support insecure HTTP Music Locker connections in the production release.

When you configure and use a Music Locker server, WoolAmp sends the credentials and library/media requests required to communicate with that server. Music Locker credentials are stored locally using Android encrypted storage and are used for the server you selected; they are not sent to WoolAmp's entitlement service.

Music Locker media is streamed or cached directly between your device and the server/media endpoint you configured.

## 6. Google Play Billing and lifetime unlock

WoolAmp offers a 15-day full-feature trial and a one-time lifetime unlock through Google Play.

Google Play is the purchase and localized-price authority. WoolAmp does not receive or store your payment-card number, bank information, or other payment-instrument credentials.

For purchase verification, the Android client receives a Google Play purchase token and sends it to WoolAmp's entitlement service over HTTPS. The service processes the raw token transiently to verify the purchase with Google Play and, when required, acknowledge it with Google Play. **The raw purchase token is not persisted in WoolAmp's entitlement database.**

WoolAmp stores a cryptographic SHA-256-derived hash of the purchase token when persistent purchase identity is required for the lifetime entitlement and device allowance.

## 7. Play Integrity and pseudonymous licensing identifiers

WoolAmp uses Google Play Integrity and a Railway-hosted entitlement service to protect the trial and lifetime unlock from simple reset/replay abuse.

The Android client creates a pseudonymous app-scoped device-binding value derived locally from Android/application information. The raw Android ID used in that derivation is not sent to the WoolAmp entitlement service by the current release implementation.

The entitlement service can receive information such as:

- the pseudonymous device-binding hash;
- an Android Keystore public key and public-key hash;
- package name and app version code;
- cryptographic challenge/nonce/signature values;
- a Google Play Integrity token; and
- for purchase verification, the Google Play purchase token and product identifier.

A P-256 private key used to prove possession remains in Android Keystore and is not exported by WoolAmp. WoolAmp's server signs accepted entitlement grants with an Ed25519 private key that does not ship in the app.

Play Integrity tokens are processed transiently and are not stored in WoolAmp's entitlement SQLite database.

## 8. Licensing ID and privacy requests

WoolAmp exposes a pseudonymous **Licensing ID** in **Settings → Privacy & Network Services → Licensing & Privacy**. It begins with `WA1-` and lets support locate the corresponding server-side entitlement/device record without asking you for Android ID, IMEI, MAC address, device serial number, raw purchase token, or private cryptographic material.

To request deletion of WoolAmp-controlled entitlement records, contact **woolamp@proton.me** and provide your Licensing ID.

A privacy deletion removes the live WoolAmp trial row, current device public-key records, the requesting device's purchase association, and any purchase-token-hash record that is no longer associated with another authorized device.

If WoolAmp has already issued a free trial to that pseudonymous device binding, WoolAmp retains only the minimum trial-eligibility record needed to prevent a deletion/reset from creating another free trial: the pseudonymous device-binding hash and the original trial start/expiry dates. This record is retained for the legitimate purpose of enforcing the one-trial policy and is not used for advertising or behavioral profiling.

Deleting WoolAmp-controlled entitlement data does not cancel or erase a Google Play purchase. Google remains the purchase authority. If you later use **Restore Purchase**, a legitimate Play purchase can be reverified and WoolAmp can recreate the necessary entitlement association.

## 9. Entitlement-service retention

WoolAmp's entitlement service follows these data-minimization rules:

- **Challenges:** random, short-lived challenges are deleted after successful consumption; expired challenges are automatically purged.
- **Raw purchase tokens:** processed transiently for Google verification/acknowledgement and not persisted.
- **Play Integrity tokens:** processed transiently and not persisted in the entitlement database.
- **Trial state:** retained as needed to administer the fixed 15-day trial and prevent repeated trials; after a privacy deletion only the minimal trial-eligibility record described above is retained if necessary.
- **Device public keys:** the current public key is retained as needed for device proof; superseded public keys are removed when a binding rotates to a new key.
- **Purchase-token hashes and purchase/device associations:** retained while needed to administer a lifetime purchase and active-device allowance; orphaned purchase hashes are removed during a privacy deletion.

## 10. Hosting logs and backups

WoolAmp's entitlement service is hosted on Railway. Railway infrastructure can process operational connection/security log information such as source IP address, user agent, request path/method, status, timing, and byte counts according to Railway's service configuration and retention practices.

WoolAmp does not intentionally write source IP addresses or request bodies into its entitlement SQLite database.

If scheduled Railway Volume backups are enabled, a record removed from the live SQLite database may remain in an existing backup snapshot until that backup expires under the configured backup schedule.

## 11. Local application data

Depending on the features you use, WoolAmp can store app-private information including:

- local music-library metadata;
- playlists, favorites, play counts, exclusions/tombstones, and library state;
- DSP, equalizer, playback, output, and application settings;
- presets and headphone-profile selections;
- skins and skin-library settings;
- lyrics and enriched metadata/artwork that have been downloaded;
- Music Locker server configuration and encrypted credentials;
- signed entitlement grants and Android Keystore key material; and
- a local crash report if WoolAmp terminates unexpectedly.

Most persistent app-private data remains until WoolAmp removes/replaces it, you use a relevant removal/reset action, you clear WoolAmp's app data, or you uninstall the app. Android-managed cache data can be cleared separately.

Clearing WoolAmp's app data or uninstalling WoolAmp does not itself delete your original music files merely because WoolAmp previously indexed them.

## 12. Crash information, analytics, and advertising

The current WoolAmp beta does **not** contain an advertising SDK or remote behavioral analytics SDK.

WoolAmp does **not** automatically upload its local crash report to WoolAmp, Railway, or a third-party crash-reporting service. A local crash report can contain technical exception/stack information and remains in WoolAmp's private app storage unless you deliberately provide diagnostic information for support.

Release builds avoid writing the full local crash stack trace to Android Logcat.

## 13. Security

WoolAmp uses HTTPS for its entitlement service and release Music Locker connections, Android application-private storage, Android Keystore for device proof, and encrypted local storage for supported Music Locker credentials.

No internet service or storage system can be guaranteed perfectly secure, but WoolAmp is designed to avoid collecting information that is unnecessary for the feature being used.

## 14. Third-party services

Features you choose to use can communicate with services operated by other organizations, including Google Play, Railway, metadata/lyrics/artwork providers, Radio Browser, internet radio stations/CDNs, and self-hosted servers you configure.

Those services may process information under their own privacy policies and terms.

## 15. Children's privacy / target audience

WoolAmp is a general-purpose music player and does not use advertising or behavioral analytics. Target age groups are declared separately in Google Play. If a release includes child age groups in its target audience, WoolAmp will apply the additional legal and Google Play requirements that apply to that audience before distribution.

## 16. Changes to this policy

This policy may be updated when WoolAmp's features, service providers, or data practices change. Material changes will be reflected in the published policy and, where appropriate, in the app.

## 17. Contact

App: **WoolAmp**
Privacy/support email: **woolamp@proton.me**
Support: **https://woolamp.github.io/support.html**
