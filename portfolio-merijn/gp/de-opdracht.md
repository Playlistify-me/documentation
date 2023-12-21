# De opdracht

De huidige software voor het bijhouden en invoeren van scores voor het Leffe Circuit is verouderd en niet functioneel. Op het moment wordt er alleen nog maar gewerkt met handmatige calculatie van punten en deze invoeren in een excel bestand. Dit neem tijd in beslag en is veel repetitief werk, en kan dus geautomatiseerd worden.&#x20;

De vraag is of wij een webapplicatie kunnen maken, welke scores van de MijnKNLTB website af haalt, de juiste berekeningen maakt voor het aantal punten, en deze punten voor het Leffe Circuit inzichtelijk maakt voor leden van Fellenoord. Dit betekent: het maken van een scraper, het bijhouden van scores per jaargang van de competitie, het opzetten en juist inrichten van een database/backend en een website waar leden van fellenoord hun scores kunnen zien.&#x20;

Het huidige ecosysteem van (de vernieuwde) website van Fellenoord wordt gemaakt met NextJS (Front-end website) en NestJS (back-end API), en een PostgreSQL database. Wij hebben er voor gekozen om dit in de grootste lijnen te volgen, waarbij de PostgreSQL database vervangen is door een MySQL database (voornamelijk in verband met de hosting mogelijkheden).
