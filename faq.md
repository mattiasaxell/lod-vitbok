# Vanliga frågor

1. [Hur förhåller sig RDF till XML?](#rdf-och-xml)
2. [Vad är för- och nackdelar med RDF kontra XML?](#rdf-kontra-xml)
3. [Hur förhåller sig RDF till CSV?](#rdf-och-csv)
4. [Vilken förvaltningsbörda medför RDF och länkade data?](#forvaltningsborda)
5. [Hur konverterbar är RDF?](#konverterbar)
6. [Vilka är de viktigaste skillnaderna mellan RDF och en relationsdatabas? Nackdelar? Fördelar? Kostnader?](#rdbms-vs-rdf)
7. [Hur hanterar man data som kräver licens för åtkomst?](#data-med-licens)
8. [Men våra data är inte av tillräckligt bra kvalitet, kan vi släppa ut dem i det tillstånd de är nu?](#kvalitet)
9. [Tappar vi inte kvalitetskontroll med länkar?](#kvalitetskontroll)
10. [Ska vi samla ihop länkade data eller lämna i källan?](#samla-lankar)
11. [Hur integrerar man bäst med en CMS?](#cms-integration)

## <a name="rdf-och-xml"></a>Hur förhåller sig RDF till XML?

XML är ett flexibelt dataformat som klarar av att uttrycka i stort sett vad som helst. Man kan jämföra XML med linjerat papper, det ger ett visst stöd och förenklar maskinell hantering i jämförelse med att skriva direkt på olinjerat papper. XML används idag för att representera allt från böcker till affärstransaktioner.

RDF å andra sidan är en datamodell som används för att uttrycka påståenden om ting. RDF kan uttryckas med hjälp av XML, som JSON, eller något annat format (en del format är skapade från grunden för att passa RDF istället för att utgå från XML eller andra "linjerade papper").
Det finns dock en likhet mellan RDF och XML som kan vara förvirrande. Båda språken är designade för att kunna hantera vilken information som helst. Skillnaden är att RDF kommer med en minimal informationsmodell (grammatik) och en semantik (tolkning) som ger stöd för att uttrycka information på ett enhetligt sätt. I RDF handlar allt om påståenden om ting och relationer mellan ting på ett sätt som bäst beskrivs som en graf av noder och typade bågar mellan noder. I XML är grunden istället en hierarki av data, men det finns ingen semantik (tolkning) av vad det innebär att ordna data i en sådan hierarki.

## <a name="rdf-kontra-xml"></a>Vad är för- och nackdelar med RDF kontra XML?

Vi tänker oss att vi ska uttrycka en ny mängd information, t.ex. information om personbilar och vem de är registrerade på. Vi jämför det normala sättet att uttrycka detta i RDF med det naturliga sättet i XML. I XML är det naturliga att skapa ett nytt XML uttryck som är specifikt för denna informationsmängd. (Notera att det alltså inte är RDFs eget XML uttryck vi jämför med då detta inte är en motsättning.) Om det finns ett etablerat XML uttryck för att beskriva just personbilar och vem de är registrerade på så har vi tur och kan återanvända detta uttryck direkt. Tyvärr är återanvändning av XML uttryck mellan olika situationer inte bara ovanligt utan också ofta ganska svårt. Den huvudsakliga orsaken har att göra med att det är vanligt med behov av olika anpassningar i förhållande till vad som formatet ursprungligen var avsett för. I detta fall skulle det kunna vara att man vill använda personnummer istället för den amerikanska motsvarigheten (socials security number) vilket riskerar att validering och existerande mjukvara inte fungerar som tänkt längre.

När vi istället uttrycker informationsmängden i RDF behöver vi inte hitta en perfekt matchning, istället kan vi leta efter relevanta vokabulärer som kan användas för att uttrycka delar av informationen. Den vanliga situationen som man ofta hamnar i är att man kan kombinera existerande vokabulär med en del egna vokabulär. I detta fall kan man använda FOAF vokabulären ([Friend Of A Friend](http://www.foaf-project.org/)) för att uttrycka personer, COO vokabulären ([Car Options Ontology](http://semanticweb.org/wiki/Car_Options_Ontology)) för att uttrycka information om bilar och kombinera med egen vokabulär kring personnummer och hur man kopplar samman en bil med den person den är registrerad på.

Sättet man återanvänder och kombinerar vokabulärer gör att RDF har flera fördelar jämfört med XML. Det finns ett stort utbud av specialiserade vokabulärer att välja på. Betydelsen av vokabulärer är ofta noggrant beskrivna då man vill att de ska vara förståeliga utanför den kontext där de ursprungligen skapades. Återanvändning av vokabulärer gör att delar av informationen som uttrycks ofta kan förstås utanför den kontext där den definierades enbart på grund av att man redan har kunskap om en del av de vokabulärer som används.

## <a name="rdf-och-csv"></a>Hur förhåller sig RDF till CSV?

CSV är ett format för att hantera tabulär information. Dvs. om den data man har kan beskrivas i en enskild tabell kan det passa att använda CSV, annars är CSV troligen ett olämpligt val.

Även för tabulär information kan CSV vara olämpligt om man har behov av att tydligt dokumentera sitt format på ett maskinläsligt sätt. RDF klarar naturligtvis av att hantera tabulär information precis som CSV, dock innebär det ett lite större arbete med att etablera vilka vokabulärer man ska använda. Dvs. att det tar lite mer tid att komma fram till hur varje kolumn ska uttryckas. Att lägga ner denna tid kan samtidigt vara väl investerad tid om den leder till bättre dokumenterade datauttryck och en bättre förståelse för datan i andra sammanhang.

## <a name="forvaltningsborda"></a>Vilken förvaltningsbörda medför RDF och länkade data?

Drift av IT system som hanterar RDF skiljer sig inte nämnvärt från andra IT system. Om man driftsätter inom den egna organisationen är det förstås viktigt med kunnig personal, framförallt generella kunskaper om webbarkitektur är viktiga. Om man istället förlitar sig på molntjänster blir förvaltningsbördan och behovet av intern kompetens kring drift betydligt mindre.

När det gäller uppdatering av informationsmodellen har RDF-baserade system en klar fördel över mer traditionella lösningar (t.ex. relationsdatabaser) då de inte har ett fixt schema. Dvs. att de kräver ingen omprogrammering för att anpassa sig till en förändrad informationsmodell, dock kan gammal data behöva transformeras för att fortfarande vara aktuell (det standardiserade frågespråket SPARQL är lämpligt att använda till detta).

Det är värt att notera att användning av RDF har potentialen att förenkla samarbetet mellan verksamheten och de som är ansvariga för systemförvaltningen (som förespråkas av vissa modeller eller perspektiv inom systemförvaltning, t.ex. Pm³ och Agil systemutveckling). Orsaken till ett sådant förenklat samarbete är att informationsmodellen både är enklare att ändra (som noterades ovan) och att den kan lagras som den är. Dvs. de som förvaltar systemet måste inte lägga energi på att översätta informationsmodellen till en annan representation internt för att kunna lagra informationen (t.ex. översätta till olika tabeller i en relationsdatabas).

RDF och länkade öppna data lösningar är per definition tillgängliga då man kan få ut beskrivningar av alla entiteter på separata webbadresser, ofta i flera olika format. Det innebär tyvärr inte med automatik att t.ex. webbapplikationer som byggs ovanpå ett länkade data lager är mer användarvängliga eller bättre följer principer för tillgänglighet som t.ex. W3C WAI. Det är dock en bra grund för att spränga in mer information i ett gränsnitt än det som syns vilket kan fångas upp av både sökmotorer och olika hjälpande teknologier.

## <a name="konverterbar"></a>Hur konverterbar är RDF?

Först låt oss konstatera att då RDF är en datamodell har det flera uttryck och format, till exempel kan man uttrycka RDF i XML, i JSON-LD och inbäddat i HTML som RDFa. Att översätta mellan dessa är enkelt och stöds av nästan alla RDF bibliotek idag.
En mer intressant frågeställning är hur enkelt det är att konvertera från ett RDF uttryck till något annat format som inte har något alls att göra med RDF. Som alltid med RDF är svaret att det beror på vilken information man har uttryckt i RDF. Om man uttryckt information om personer i RDF kan man med fördel översätta till vCard, om det handlar om vokabulärer kan kanske Claml vara lämpligt. Det finns dock ingen allmän mekanism för att göra dessa konverteringar utan det måste utvecklas för varje situation. Det är också värt att notera att om RDF vokabulären inte är helt kompatibel med målformatet så är det högst sannolikt att viss information går förlorad i samband med konverteringen. Brist på stringens i definitionen av semantiken för målformatet är en vanlig orsak till att konverteringar kan vara svåra att skriva på ett sätt som inte är beroende av sammanhanget.
Ofta finns det dock ramverk som man kan använda för att bygga konverteringen på, t.ex. för tabulär data kan man använda [OpenRefine](http://openrefine.org) eller [TARQL](https://github.com/cygri/tarql), för relationsdatabaser kan man använda [D2R](http://d2rq.org/d2r-server) osv. W3C har upprättat en rekommendation för [R2RML](http://www.w3.org/TR/2012/REC-r2rml-20120927/), ett standardiserat språk för att mappa data i befintliga relationsdatabaser till en RDF graf; språket stöds t.ex. av det ovannämnda D2R.

## <a name="rdbms-vs-rdf"></a>Vilka är de viktigaste skillnaderna mellan RDF och en relationsdatabas? Nackdelar? Fördelar? Kostnader? Utbyggbarhet vid stora informationmängder?

En traditionell relationsdatabas kräver att man etablerar ett databasschema som definierar vilka tabeller, kolumner och relationer mellan dessa som ska finnas. Detta fungerar väl när datan man hanterar är relativt uniform och den underliggande informationsmodellen inte ändras alltför ofta. En naturlig konsekvens är att relationsdatabaser inte kan hantera nya data som det inte har explicit förberetts för. En databaslösning som inte kräver ett fördefinierat databaschema är mer flexibel, men kan samtidigt blir mer svåröverskådlig.

De flesta RDF databaser fungerar utan schema och kan därmed hantera vilken information som helst så länge den kan uttryckas som påståenden om resurser identifierade med URI:er, dvs. så länge man följer RDFs abstrakta syntax.

## <a name="data-med-licens"></a>Hur hanterar man data som kräver licens för åtkomst?

Det är först viktigt att notera att frågeställningen om hur man kan använda källor vid publicering av länkade öppna data är att jämställa med annan form av webbpublicering.
I huvudsak finns tre möjliga lösningar att prövas i ordning kring källor som har specifika restriktiva licenser.

1. Noga undersöka vad licensen säger, troligtvis är det möjligt att publicera delar av en källa i anslutning till att den används. Eventuellt kan man komma undan genom att inte tillåta renodlad sökning eller bulk nedladdning av källan utan bara indirekt åtkomst till delar.
2. Begränsa åtkomst till vissa källor som länkade data baserat på vem som är användaren.
3. Rekommendera byta till en annan datakälla.

## <a name="kvalitet"></a>Men våra data är inte av tillräckligt bra kvalitet, kan vi släppa ut dem i det tillstånd de är nu?
Det kan finnas hinder på grund av lagar och regleringar som måste beaktas, till exempel personuppgiftslagen (PUL) och copyrightskydd, läs mer om detta på e-delegationens vägledning kring [vidareutnyttjande av information](http://www.vidareutnyttjande.se/). Ur ett kvalitetsperspektiv är det svårare att säga något generellt, men ofta är det bättre att komma igång med att släppa en del data och få återkoppling från andra än att på egen kammare försöka förutse alla problem. Med andra ord, ett iterativt arbetsätt är ofta att föredra även för publicering av länkade data.

Notera: att göra sina data tillgängliga som länkade data innebär inte med automatik att de måste vara öppet tillgängliga.

## <a name="kvalitetskontroll"></a>Tappar vi inte kvalitetskontroll med länkar?
Det är naturligt att kvaliteten varierar mellan datakällor då ansvariga organisationer lägger olika stor vikt vid sina data. Dessutom är det stor skillnad mellan datakällor som skapas på frivillig basis (t.ex. crowdsourcing) och de som ges ut av organisationer med avlönade experter.

Brist på kvalitet kan yttra sig både genom att datakällor periodvis är otillgängliga eller på brist i konsekvens i vilka påståenden som är uttryckta per ting. Periodvis otillgängliga datakällor går att kompensera för genom smart cachning, men brist på konsekvens är svårare.

En uppenbar lösning är helt enkelt att låta bli att länka till datakällor med för dålig kvalitet. Ett annat mer tilltalande alternativ är att välja att länka med relationer som är medvetet lösare i sin karaktär, t.ex. `rdfs:seeAlso` istället för `owl:sameAs` som får mer långtgående konsekvenser i form av maskinell bearbetning. Det är också stor skillnad mellan att länka till ting i andras datakällor och att återanvända klasser, egenskaper eller begrepp vilket i allmänhet ställer högre krav på kvalitet.

## <a name="samla-lankar"></a>Ska vi samla ihop länkade data eller lämna i källan?

Att duplicera information ska i största allmänhet undvikas, men ibland är det nödvändigt för att uppnå god användbarhet i de tjänster eller applikationer som bygger på denna information. Datakällor kan ibland vara offline eller ha dålig prestanda och ibland vill man själv ha kontroll över tillgängligheten. Kan en applikation inte byggas så att den klarar av att fungera med otillgängliga datakällor, så kan det vara angeläget att duplicera data i sin egen infrastruktur med regelbundna uppdateringar. Detta förutsätter att det är tekniskt hållbart (dvs. datamängden går att hantera), samt att datakällans licensebestämmelser tillåter en sådan användning.

[Caching servern LDCache](http://entrystore.org/ldcache/) har utvecklats av MetaSolutions för att hämta in och cacha viktiga länkade (öppna) data. Detta ger bättre kontroll över en datakällas prestanda och tillgänglighet. LDCache är ett Open Source projekt.

## <a name="cms-integration"></a>Hur integrerar man bäst med en CMS?
Det finns flera olika sätt att integrera länkade data i en CMS. En möjlighet är att låta CMS plattformen prata direkt med LD plattformen, t.ex. via specifika API:er eller direkt på databas nivån. Men i många fall kan en sådan integration vara krånglig, särskilt om plattformarna är skrivna i olika programmeringsspråk. Ett bättre alternativ är att utnyttja att länkade data i sig är ett slags API som exponeras över HTTP.

Idag erbjuder de flesta stora CMS:er ett kontrollerat sätt att utöka sin funktionalitet, typiskt genom att utveckla pluginner eller moduler. Beroende på CMS:en kan sådan ny funktionaltet införas enbart på serversidan eller också via javascript i browsern. Båda alternativen fungerar väl med integration med länkade data, gärna via färdiga bibliotek som hanterar parsning och bearbetning av länkade data uttryck.

Ibland kan också länkade data plattformar erbjuda färdiga gränssnittskomponenter, t.ex. för att lista, söka eller presentera enskilda resurser. Det är möjligt att sådana komponenter kan inkorporeras med en mindre insats (fixa enhetligt utseende via teman eller ren css) på samma sätt som man bäddar in t.ex. youtube klipp.

Vi summerar de olika integrationsmöjligheterna (där alla med fördel genomförs via någon form av plugin eller modul i respektive CMS):

1. CMS backend pratar med LD backend - ofta krångligt, undvik
2. CMS backend hämtar LD över HTTP - fungerar alltid
3. CMS frontend hämtar LD över HTTP - fungerar alltid
4. CMS frontend bäddar in färdiga LD frontend komponenter - bara om stöd finns i LD plattformen
