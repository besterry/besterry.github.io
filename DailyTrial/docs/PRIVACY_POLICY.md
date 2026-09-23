# Privacy Policy for "Daily Trial"

**App:** "Испытание дня" / "Daily Trial", package name `com.dailytrial.app`
**Developer:** MobileWave Dev
**Privacy contact:** mobilewave.dev@gmail.com
**Effective date:** 23 September 2026
**Current version of this document:** https://git.fdhub.work/DailyTrial/privacy-policy.html

This policy describes what data the Daily Trial app accesses, how it uses that data, who it is
shared with, how long it is kept and how you can have it deleted. It is written from how the app
and its server actually work, not from a template.

---

## 1. In short

- No registration is required. You can play without signing in to any account.
- The app creates a random installation identifier so that your results can appear on the
  leaderboard and your progress can be restored.
- Signing in with Google is optional. It exists only so that your progress survives a reinstall
  or a change of phone.
- The app contains ads and analytics. Both run on third-party Yandex services, and those
  services receive your device's advertising identifier and technical information about the
  device.
- The app does not request access to location, camera, microphone, contacts, calendar, photos,
  files or messages. It holds no such permissions at all.

---

## 2. Data that stays only on your device

The app stores the following in its own private storage on the device:

- your daily streak state, including your record and streak freezes;
- your game history, up to the 200 most recent rounds: date, mode, the hidden word, the words
  you entered, the number of attempts, the duration, the number of hints;
- your total experience points, unlocked achievements, chosen avatar;
- counters of rounds played and hints used;
- settings: language, theme, notifications, colorblind mode, companion cat;
- a counter of interstitial ads shown today, so the app can respect its own limit;
- the random installation identifier and the request signing keys;
- your leaderboard nickname;
- if you signed in with Google: your Google account identifier and e-mail address, so that the
  profile screen can show which account is signed in.

This data is removed when you uninstall the app or clear its data in Android settings.

### 2.1 Android backup

The app uses standard Android backup. If backup is also enabled in your device settings, the
operating system copies the settings file described above into your Google account backup and
transfers it when you move to a new device. That copy therefore includes the installation
identifier, the request signing keys, the nickname, the game history and, if you signed in with
Google, your Google account identifier and e-mail address.

On devices running Android 12 and later, the app additionally requires that the cloud copy only
be created when it can be encrypted on the device itself, with a secret your device holds rather
than us or Google. In practice that means the device has a screen lock. Where that is not
possible, no cloud copy is created at all, and a reinstall starts from scratch.

That copy is controlled by Google and by your device's backup settings, not by the app. You can
turn it off in Android settings.

---

## 3. Data the app sends to our server

Our server runs on the Vercel platform at `https://daily-trial-api.vercel.app`. It is the only
network address our own code contacts.

### 3.1 Identifier

Until you sign in with Google, your identity on the server is a random installation identifier:
a value generated randomly on your device on first launch. It is not derived from the
advertising identifier, serial number, IMEI, MAC address or any other hardware identifier, and
on its own it does not say who you are.

After you sign in with Google, your identity on the server becomes the stable identifier of your
Google account. All subsequent records on the server are tied to it.

### 3.2 What is sent

| What | When | Why |
|---|---|---|
| Installation identifier or Google account identifier | On every request to the server | So the server knows whose record it is |
| Nickname | When a result is submitted and when you rename yourself | To show you on the leaderboard |
| Daily result: date, number of attempts, duration | Only after a **solved** daily challenge. Lost days are never sent | Leaderboard ranking |
| Avatar and total experience points | When you change your avatar and after rounds that change experience | League badge and avatar on the leaderboard |
| Progress snapshot | After signing in with Google and after progress changes | Cloud save, so progress survives a reinstall or a change of phone |
| Google ID token | Only when signing in with Google | To prove that you really own that account |
| IP address | On every request, automatically, as with any internet connection | Rate limiting and protection against cheating |

### 3.3 What the progress snapshot contains

If you enabled cloud save by signing in with Google, a full snapshot of your game progress is
sent to our server: your streak state, up to the 200 most recent rounds including the hidden
words, all the words you entered, timestamps and durations, your endless mode record, your total
experience points, the list of achievements you unlocked and your chosen avatar.

The server does not parse the contents of this snapshot and stores it as a single opaque block.

### 3.4 About your e-mail address

When you sign in with Google, your device sends our server a Google ID token. Our server
verifies it with Google, reads the account identifier and the e-mail address from it, and
returns them to your device.

**Your e-mail address is not stored on our server.** It is kept only on your device, so the
profile screen can show which account is signed in, and it is included in the Android backup
described in section 2.1.

The Google ID token itself, which is issued by Google, may by the standard also contain your
name and a link to your profile picture. Those fields pass through our server in transit only:
we do not read them, do not use them and do not store them.

### 3.5 About your IP address

Your connection's IP address is processed in two places:

1. In the logs of the Vercel platform that hosts our server. Those logs record the IP address,
   the client software used, the method, the path, the query parameters and the response code.
   Request bodies are not written to the logs. The retention period is set by the platform plan:
   one hour on the plan the server currently uses. If the plan changes, this policy will be
   updated.
2. In our own storage, as part of a technical rate limiting key. Such a key is created when a
   device first registers, when you sign in with Google, and on every read of the leaderboard,
   which in practice means on almost every app launch. It holds only the IP address and a
   request counter, is kept for **one hour** and is then deleted automatically. Rate limiting is
   there so the leaderboard cannot be harvested automatically, and to protect the server from
   cheating.

---

## 4. What other players can see

The leaderboard is public. Other players see your nickname, your avatar, your experience points
and league badge, your score, and on the daily board also your number of attempts and your
solving time.

Other players **cannot see** your e-mail address, your installation identifier, your Google
account, the hidden words, the words you entered or your game history.

The default nickname is generated by the app and contains no personal data about you. If you
replace it with your real name or other information about yourself, that becomes public. Please
choose your nickname with that in mind.

---

## 5. Third-party services in the app

The app uses two third-party sets of libraries. Both belong to the Yandex group. They collect
data on their own, through their own code, and this begins at the first launch of the app,
whether or not you ever see a single advertisement.

### 5.1 Yandex Mobile Ads, advertising

Ads are shown only in endless mode: an interstitial between rounds, and a rewarded video that
you can choose to watch in exchange for a hint or an extra attempt. **There are no ads in the
daily challenge.**

According to the vendor's documentation, this set of libraries collects and shares with Yandex
as a third party the device advertising identifier or another device-level identifier, for the
purpose of showing and measuring advertising. Yandex's advertising privacy policy additionally
lists that in publishers' apps it processes the IP address, advertising identifiers, the device
identifier and other device parameters, information about the operating system version, the
internet connection type, SIM card data and third-party advertising system identifiers.

The controller of that data is Yandex Europe AG, Werftestrasse 4, 6005 Lucerne, Switzerland.
Data may be disclosed to partners to the extent necessary to serve ads, including Google, and
transferred to other countries, including Russia. The vendor states no fixed retention period.

We explicitly deny this set of libraries personalization: the app calls `setUserConsent` with
"no" on every launch, because we have no consent screen and nothing to ask about. According to
the vendor's documentation this does not turn ads off, it removes personalization and targeting.
We also explicitly turn off its own automatic forwarding of ad impression data into AppMetrica:
that is not the same figure described in section 5.2 as game events, it is a separate channel
that ships enabled by default in the library, which we do not use and do not read ourselves.

Vendor documentation: https://ads.yandex.com/helpcenter/en/dev/android/app-privacy-android
Privacy policy: https://yandex.com/legal/international_ads_privacy_policy/en/

### 5.2 AppMetrica, analytics and crash reports

We send AppMetrica events about how the app is used: launch, opening the daily challenge,
submitting an attempt, finishing a round, a change of streak, tapping the share button,
starting endless mode, showing and watching an ad, scheduling and opening a notification,
switching tabs. Attached to those events are the day index since installation, the current
streak, whether today's challenge has been played, the app version, the content version, the
total number of rounds played, plus parameters of the specific event: number of attempts,
duration, whether it was solved, the difficulty tier and similar.

**These events do not include** the hidden words or the words you entered, your nickname, your
e-mail address or your installation identifier.

In addition, the AppMetrica libraries collect data on their own, mostly under their default
settings. We changed one of those settings ourselves, noted below. According to the vendor's
documentation and the actual composition of the library set, this is:

- app crash reports, including stack traces;
- diagnostics and technical information about the device, including the operating system
  version, the screen type, and the battery level for crash analysis;
- device identifiers, including the Google advertising identifier and AppMetrica's own device
  identifier. The App Set ID is collected separately and directly by the Yandex Mobile Ads set
  of libraries (section 5.1); we deliberately excluded the AppMetrica module that would
  otherwise derive its own device identifier from the App Set ID from the app's build, so
  AppMetrica no longer relies on that identifier;
- device model and manufacturer, device language, mobile operator name and the MCC and MNC
  codes, internet connection type;
- session and installation identifiers, and the installation timestamp;
- the app's install source from the app store;
- **the IP address.** By the vendor's own statement, AppMetrica stores users' full IP addresses
  by default and uses them to determine a user's location more precisely. Masking is a separate
  setting on the service side, and **we have turned it on**: on 20.09.2026 the app's AppMetrica
  settings were changed to "Do not store full IP addresses of users from the EU". For users in the
  EU the vendor does not store the full IP address. The setting does not apply outside the EU,
  where the IP address is handled by the vendor as described above.

AppMetrica does not collect location through the system location services: the app holds no
location permissions, and the vendor's corresponding setting is disabled by default.

The data is transferred to Yandex and stored on Yandex servers in the European Union and in the
Russian Federation. The vendor states that data is encrypted in transit. The vendor does not
publish a retention period.

Vendor documentation: https://appmetrica.yandex.com/docs/en/data-security/google-data-safety
On IP address storage: https://appmetrica.yandex.com/docs/en/data-security/ip-masking

### 5.3 How to limit advertising data collection

There is currently no separate in-app switch to turn off ads and analytics. You can limit the
use of the advertising identifier through Android itself: Settings, Privacy, Ads, where you can
reset the advertising identifier and opt out of personalized advertising. The exact names of
these items differ between devices.

---

## 6. Other recipients of data

The complete list of parties that receive data in connection with the app:

| Who | What they receive | Why |
|---|---|---|
| Vercel Inc. | All of the app's network requests to our server, including the IP address | Hosting of our server |
| Upstash | The contents of our database: identifiers, nicknames, avatars, experience points, results, progress snapshots, technical rate limiting keys | Storage for our server |
| Yandex Europe AG and the Yandex group | See sections 5.1 and 5.2 | Advertising and analytics |
| Google LLC | Verification of the Google ID token on sign-in; the sign-in flow itself through Google Play services; the Android backup, if it is enabled; the advertising identifier, which Google Play services provide | Google sign-in, backup, advertising identifier |
| Other players | Nickname, avatar, experience points, score, daily result | Leaderboard |
| The app you choose yourself in the share menu | The result image and the text | Only when you take that action |

We do not sell your data and we do not pass it to anyone other than the parties listed above.

---

## 7. Why we process data

- App functionality: saving your progress, streak, achievements and settings.
- Leaderboard and the competitive part: publishing your result under the nickname you chose.
- Cloud save: restoring your progress after a reinstall and on a new device.
- Anti-cheating: signing requests and limiting their rate by IP address and identifier.
- Analytics: understanding which features are used, where people stop playing, and whether
  something broke after an update.
- Crash reports: finding and fixing errors.
- Advertising: showing and measuring advertisements in endless mode.

---

## 8. Retention periods

| Data | Where | How long |
|---|---|---|
| All local data, including game history and e-mail address | On the device | Until you uninstall the app, clear its data or sign out |
| Daily result on the daily leaderboard | Our server | 3 days, then deleted automatically |
| Weekly points | Our server | 12 days, then deleted automatically |
| Duplicate scoring guard | Our server | 3 days |
| Nickname, avatar, experience points | Our server | Indefinitely, until you request deletion |
| Progress snapshot | Our server | Indefinitely, until you request deletion. There is deliberately no automatic expiry here: losing a player's real save is worse than keeping it longer than strictly needed |
| Technical rate limiting keys containing the IP address | Our server | 1 hour |
| Server logs containing IP addresses | Vercel | 1 hour on the current plan |
| Analytics data and crash reports | AppMetrica | The vendor publishes no retention period. It is determined by Yandex |
| Advertising data | Yandex Europe AG | The vendor states no fixed period. In its wording, as long as required for the purposes of processing |
| Android backup | Google | Determined by Google and by your device settings |

---

## 9. Deleting your data

### 9.1 Delete everything locally

Uninstall the app or clear its data in Android settings. Everything in section 2 is erased from
the device. If you also want that data removed from the Android backup, turn off backup for the
app in Android settings.

### 9.2 Delete your data on our server

The app provides an in-app path to data deletion: the profile screen has an option to delete
your account and data, with a confirmation step. It deletes your nickname, avatar, experience
points, cloud progress save and your entries in the active leaderboards from our server, and on
the device it unlinks the Google account and erases local data.

You can request the same thing without the app, on the deletion request page:
https://daily-trial-api.vercel.app/delete-account-en.html

Requests are processed within 30 days.

A technical note: if you used the app before signing in with Google, the records you created
before signing in (your leaderboard entries and the nickname stored with them) were tied to the
previous random installation identifier and are not migrated when the account is linked. The
in-app deletion currently removes the data of the signed-in account. Leaderboard entries from
before sign-in disappear automatically when the leaderboard window expires: 3 days for the daily
board and 12 days for the weekly board. To have the remaining pre-sign-in records removed as
well, write to the address in section 13 and we will delete them.

### 9.3 Delete your data held by third-party services

- **Yandex Mobile Ads.** Rights of access, rectification and erasure are exercised by contacting
  Yandex Europe AG through the Yandex support form referenced in Yandex's advertising privacy
  policy: https://yandex.com/legal/international_ads_privacy_policy/en/
- **AppMetrica.** The deletion mechanism documented by the vendor applies to the app's data as a
  whole and is carried out by the developer. The vendor does not publish a mechanism for
  deleting one individual user's data on request. If you send us such a request, we will pass it
  to the vendor and tell you the outcome.

---

## 10. Security

- All communication between the app and our server uses HTTPS.
- Every request that changes your data is signed with a key issued specifically to your
  installation. The master secret that key is derived from exists only on the server and is
  never sent to the device or stored in the app.
- The cloud save can only be read or written with a signed request. Without a signature it is
  inaccessible.
- Request rates are limited, to make brute force and score inflation harder.
- Local data is kept in the app's internal storage, which by Android's rules other apps cannot
  access.
- The third-party library vendors state that data is encrypted in transit: HTTPS/TLS for Yandex
  Mobile Ads and AES-128 for AppMetrica.

An honest caveat: no protection is absolute. Request signing in this app is designed to stop
obvious score cheating, not to withstand a determined attack.

---

## 11. Children

The app is not intended for and is not directed at children. We deliberately do not collect
children's data. If you believe a child has provided us with data, write to us using the contact
in section 13 and we will delete it.

---

## 12. Changes to this policy

If the set of data we process changes, we will update this document and change the effective
date at the top. Material changes will also be reflected in the app's release notes in the
store.

---

## 13. Contact

For any question about your data, and to access, correct or delete it:

**Developer:** MobileWave Dev
**Privacy e-mail:** mobilewave.dev@gmail.com

This is also the address for deletion requests, if you prefer to write rather than use the page
in section 9.2.
