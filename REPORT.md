## Här är MFA/TOTP aktiverad och verifierad med en autentiseringsapp:

![Alt-text](MFA_Activated.jpg)

## Kontolåsningen är aktiverad och testad (loggade in tills den är låst):

![Alt-text](Locked_Out.jpg)

## Här visas att MFA/TOTP krävs vid inloggning (om det är aktiverat):

![Alt-text](MFA_Required.jpg)

## Inloggad:

![Alt-text](Logged_In.jpg)

## Här loggar jag in med en återställningskod (recovery code) som genererats i samband med att MFA/TOTP aktiverades:

![Alt-text](Login_With_Recovery_Code.jpg)

## Inloggningsskärmen efter inloggning med recovery code:

![Alt-text](Logged_In_With_Recovery_Code.jpg)

# Motiveringar

1. **Varför TOTP och inte SMS?**\
  Jag valde TOTP framför SMS eftersom SMS-baserad MFA är känsligare för bland annat
  SIM-kapning och social engineering mot mobiloperatörer, där en angripare kan få
  tillgång till offrets telefonnummer och därmed MFA-koderna. TOTP genererar istället koder
  lokalt i en autentiseringsapp och är därför inte beroende av mobilnätet eller operatören
  på samma sätt. Varken TOTP eller SMS skyddar dock fullt mot phishing och realtidsproxying,
  där en angripare kan vidarebefordra en användares kod till den riktiga servern i realtid.
  Trots att SMS är bättre än ingen andra faktor alls bedömde jag att TOTP ger en bättre
  säkerhetsnivå för den här applikationen.

2. **Antal försök och låsningstid**\
  Jag valde 5 misslyckade försök och en låsningstid på 5 minuter som en avvägning mellan 
  säkerhet och tillgänglighet. För en legitim användare räcker 5 försök — antingen fyller en 
  lösenordshanterare i rätt lösenord direkt, eller så täcker det in en vanlig felskrivning — 
  samtidigt som det håller nere hur många gissningar en angripare hinner göra innan kontot låses, 
  vilket gör brute-force-attacker svårare. 5 minuter är dessutom ASP.NET Core Identitys eget 
  standardvärde för låsningstiden: tillräckligt lång tid för att hindra en angripare från att 
  göra många försök på kort tid, men kort nog för en legitim användare som bara behöver vänta en 
  stund. Kortare låsningstider är inte rekommenderat, eftersom det kan leda till att en 
  angripare kan göra fler försök inom samma tidsperiod. Längre än 5 minuter skulle göra 
  det svårare för en angripare att få tillgång till kontot, men det skulle också leda till mer
  besvär för en legitim användare som råkar skriva fel lösenord flera gånger i rad.

# Recovery codes

3G587-TF2C4\
HM3C8-DFX9Q\
VBGN7-WJKP2\
MMCVW-27QK6\
DG45M-8CXFV\
R73XY-DN352\
342MW-32QQ9\
5D75T-GPFCD\
JTPFH-2M8GK\
7XMJV-388YC

## Login

<test@minapp.se> / Sommar2024!
