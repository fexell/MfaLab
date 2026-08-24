# MfaLab

Startrepo för **övning 5.3: MFA i .NET med TOTP, kontolåsning och recovery codes** i kursen IT-säkerhet för utvecklare.

Det här är en Blazor Web App på .NET 10 med ASP.NET Core Identity och EF Core (SQLite). All plumbing finns på plats: användare, inloggning, tvåfaktor och recovery codes. Din uppgift är att aktivera TOTP, verifiera det med en autentiseringsapp och sedan konfigurera kontolåsning och recovery codes. Hela uppgiftstexten med stegen ligger i Learnpoint.

## Kom igång

### Förutsättningar

- .NET 10 SDK
- En autentiseringsapp i mobilen, till exempel Microsoft Authenticator eller Google Authenticator

### Kör appen

```powershell
dotnet run
```

Öppna adressen som skrivs ut (till exempel `https://localhost:7288`). Logga in med testanvändaren nedan och gå sedan till **Konto → Two-factor authentication → Set up authenticator app**.

### Testanvändare

En användare sås automatiskt vid första starten, så du slipper registrera dig först.

| Fält | Värde |
|------|-------|
| E-post | `test@minapp.se` |
| Lösenord | `Sommar2024!` |

## Var du gör vad

| Steg i övningen | Var i koden eller appen |
|-----------------|-------------------------|
| Steg 2–5, aktivera och verifiera TOTP | Kör flödet i appen: **Konto → Two-factor authentication → Set up authenticator app**. Koden bakom ligger i `Components/Account/Pages/Manage/EnableAuthenticator.razor` (`GetAuthenticatorKeyAsync`, `VerifyTwoFactorTokenAsync`). |
| Steg 7, kontolåsning | Två ställen. **1)** `Program.cs`, `TODO steg 7`: lägg `options.Lockout`-raderna i options-lambdan för `AddIdentityCore`, se [AddIdentityCore i stället för AddIdentity](#addidentitycore-i-stället-för-addidentity). **2)** `Components/Account/Pages/Login.razor`, cirka rad 124: byt `lockoutOnFailure: false` mot `true`. Mallen skickar redan en låst användare till `/Account/Lockout`. |
| Steg 8, recovery codes | `Components/Account/Pages/Manage/GenerateRecoveryCodes.razor` använder `GenerateNewTwoFactorRecoveryCodesAsync`. Koderna lagras hashade av Identity och fungerar en gång var. |
| Steg 9, motiveringarna | Skriv dem i `REPORT.md` (skapa filen) eller i din labbrapport. |

## Bra att veta

### QR-koden fungerar direkt

Standardmallen från Microsoft renderar ingen QR-kod, den visar bara en URI och hänvisar till ett externt bibliotek. Det här repot genererar QR-koden serverside med QRCoder och visar den som en färdig bild på uppsättningssidan. Ingen CDN, inget JavaScript-bibliotek att haka i. Det är ändringen i `Components/Account/Pages/Manage/EnableAuthenticator.razor`.

### AddIdentityCore i stället för AddIdentity

Uppgiftstexten visar `AddIdentity<ApplicationUser, IdentityRole>(...)`. Blazor-mallen registrerar Identity med `AddIdentityCore<ApplicationUser>(...)` i stället, vilket är det normala för en Blazor-app utan roller. Lockout-inställningarna sätts på exakt samma `options.Lockout`-objekt, så resonemanget i uppgiften gäller oförändrat. Kodsnutten i uppgiften är alltså rätt i sak, den sitter bara i en app som redan valt Blazor-varianten.

### Databasen

SQLite-filen skapas automatiskt vid första körningen. Vill du börja om från en ren databas, stäng appen och radera `.db`-filen, så sås testanvändaren på nytt vid nästa start.
