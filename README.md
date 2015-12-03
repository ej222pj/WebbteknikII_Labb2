# Rapport för WebbteknikII_Labb 2
EJ222PJ
Eric Jennerstrand 

## Säkerhetsproblem

#### Inte Hashade Lösenord!
Lösenord ska alltid vara hashade i en databas, men i denna applikationen sparas lösenorden i klartext. Detta betyder att om databasen blirr hackad får hackaren tillgång till alla lösenord och emailadresser. Om en användare då har samma lösenord på flera webbsidor har hackaren tillgång till de webbsidorna också. Om alla lösenord istället hade blivit hashade med ett unik salt. Om en hackare då hade fått tag i lösenorden hade det inte gjort något för att det är nästan omöjligt att få fram ett lösenord som har blivit hashat.  [1]

#### SQL-injections
Det är möjligt vid inloggningen att göra ett så kallat "SQL-injection", det innebär att man inte behöver skriva rätt mail eller lösenord. Det går att skicka en sql fråga som tex 
" ' OR '1'='1 " och man kommer att bli inloggad, för att applikationen tror att det är en giltig inloggning. Detta är inte bara dåligt för att man kan logga in utan giltig inloggning utan det går även att använda denna metoden för att förstöra eller ändra data och det skulle även gå att ta bort hela databasen. För att förhindra detta kan man använda speciella APIer, det går även att förhindra att användaren skriver in vissa tecken och på de sättet stoppa SQL-injections. [2] [3]

#### Öppna funktioner
Det är möjligt att anropa funktioner med en url direkt ifrån webbläsaren utan att behöva logga in. Det går på detta viset att få tag i tillexempel alla meddelanden i form av ett json-objekt genom att skriva http://localhost:3000/message/data i URLen. För att förhindra detta kan applikationen neka tillgång till alla funktioner, för att sedan tilldela rättigheter till de olika inloggningarna. [4]

#### Nedladdningsbar Databas
Det går att ladda ner databasen, vilket medför en riktigt stor risk för alla användare. Med tanke på att man får full tillgång till alla användaruppgifter och meddelanden. Klienten har också ett krav på att alla meddelanden ska vara oåtkomliga för de som inte har inloggningsuppgifter. Detta kravet uppfylls inte när det går att ladda ner hela databasen. [4]

#### JavaScript i meddelanden
Det finns inget som hindrar en användare att göra en XSS attack genom att tillexempel göra en knapp eller länk i ett meddelande som gör en redirect till en annan sida där en elak användare kan spara knapptryckarens cookie och sen använda den för att logga in i knapptryckarens identitet. För att skydda sig mot detta kan man förhindra användaren att skriva in special tecken som < och >. Men om dessa tecken behövs går det att göra om tecken till HTML tecken kodning. [5] [6]

#### Dålig sessions hantering
När en användare loggar ut förstörs inte sessionen vilket innebär att det går att använda backåtknappen eller skriva in en url som används när man är inloggad för att bli inloggad på samma profil igen. Detta medför att användare 1 kan logga ut och sedan kan användare 2 börja använda datorn och logga in igen på användare 1s profil. Detta går att förhindra på ett enkelt sätt genom att se till att sessionen förstörs när en användare loggar ut. [7]

## Prestandaproblem

#### Onödiga HTTP-anrop
En webbapplikation borde göra så få HTTP-anrop och i denna applikation finns det länkar till resurser som inte finns på servern. Därför kommer inte applikationen att hitta dessa resurser och kommer därför få en 404. I detta fallet hittar jag 3 resurser som ger en 404. "materialize.min.css", "materialize.js" och "ie-10-viewport-bug-workaround.js" går inte att hämta och borde därför inte länkas in. Anledning till att dessa borde plockas bort är för att de blir en snabbare responstid på sidan. [8]

#### JavaScript i header
All javascript kod laddas in i headern vilket gör att om det är stora filer som behöver läsas in kommer sidan att vara helt vit medan scriptet läses in. Om javascriptet istället hade legat i slutet av <body> taggen eller ännu bättre i en footer, hade sidan börjat rendera sidan och visat informationen. [9]

#### Inline kod
I applikationen finns det mycket inline kod, i alla vy filer är CSSen och lite JavaScript skriven direkt i body taggen och viss javascript också. Gör man på detta sättet blir responstiden lite kortare för att webbläsaren behöver inte hämta inlänkade filer. Men problemet med inline kod är att CSS och JavaScript sparas inte i cachen och man kan få skriva dubbel kod som i index.html och admin.html. Hade all CSS och JavaScript istället länkats in externt hade den koden automatiskt sparats i cachen och inte behövts läsas in vid varje request. Kort sagt: Länka in CSS I header och JavaScript så långt ner i html dokumentet som möjligt för att dessa filer ska kunna cachas. [10]

#### Logout knappen
Logout knappen visas hela tiden, även när en användare inte är inloggad. Det är onödigt att den visas när man inte är inloggad för det kan uppstå förvirring hos användarna. Det blir också dubbel JavaScript kod som är onödig att läsa in. Det hade räckt med att bara visa logout knappen när en användare är inloggad. [11]

## Egna övergripande reflektioner 

#### Meddelanden visas inte direkt
Efter att en användare har loggat in visas inte de existerande meddelandena förens använderen har skrivit ett nytt meddelande. Alla meddelanden borde visas direkt när en användare loggar in.

#### Validerings meddelande
Det saknas helt validerings meddelanden vid inloggning vilket gör att inloggningen inte är användarvänlig. Applikationen borde visa om eposten inte matchar ett konto eller om lösenordet är felaktigt.

#### Radbrytning i meddelanden
Det saknas radbrytning i meddelandena. Om en användare skriver ett långt ord kommer inte ordet att byta rad utan visas utanför meddelanderutan. 

#### Egna reflektioner om labben
Jag tycker att denna labben har varit väldigt intressant och den har gett mig en tankeställare om mina egna applikationer som jag behöver titta över nu. Även att denna applikationen var väldigt överdriven med sina fel kan jag tänka mig att det är många gånger som programmerare missar några av dessa felen. Jag gillade OWASPs top 10 lista, det är ett riktigt bra sätt gå igenom iallafall de 10 vanligaste felen en applikation kan ha och jag kommer ha med mig den en lång tid framöver.

## Referenser 
[1] "OWASP Password Storage Cheat Sheet" [Online] Tillgänglig: https://www.owasp.org/index.php/Password_Storage_Cheat_Sheet
[Hämtad: 30 november 2015]

[2] "OWASP Top Ten Project A1" [Online] Tillgänglig: https://www.owasp.org/index.php/Top_10_2013-A1-Injection
[Hämtad: 30 november 2015]

[3] "OWASP SQL Injection Prevention Cheat Sheet" [Online] Tillgänglig: https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet
[Hämtad: 30 November 2015]

[4] "OWASP Top Ten Project A7" [Online] Tillgänglig:https://www.owasp.org/index.php/Top_10_2013-A7-Missing_Function_Level_Access_Control
[Hämtad: 30 November 2015]

[5] "OWASP Top Ten Project A3" [Online] Tillgänglig: https://www.owasp.org/index.php/Top_10_2013-A3-Cross-Site_Scripting_(XSS)
[Hämtad: 30 November 2015]

[6] "OWASP XSS Prevention Cheat Sheet" [Online] Tillgänglig: https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet
[Hämtad: 30 November 2015]

[7] "OWASP Top Ten Project A2" [Online] Tillgänglig: https://www.owasp.org/index.php/Top_10_2013-A2-Broken_Authentication_and_Session_Management
[Hämtad: 30 November 2015]

[8] High Performance Web Sites, Essential Knowledge for Front-End Engineers
By Steve Souders 2007. s. 10.

[9] High Performance Web Sites, Essential Knowledge for Front-End Engineers
By Steve Souders 2007. s. 45-50.

[10] High Performance Web Sites, Essential Knowledge for Front-End Engineers
By Steve Souders 2007. s. 55-61.

[11] High Performance Web Sites, Essential Knowledge for Front-End Engineers
By Steve Souders 2007. s. 85-88.


