#####Git workflow
Dit document legt de git workflow van dit project uit

####Branches
Het project heeft twee persistente branches, master en dev. Op master staan alleen volledige releases, als versie 0.2 af is zal die van dev gemerged worden naar master. Eventueel kan er dan vanuit master een nieuwe branch gestart worden met fixes voor 0.2 die dan gemerged moeten worden in zowel dev als master. Er zal dus nooit direct gecommit worden naar master.

Merges naar dev komen van zogenaamde feature branches, stel dat er een feature "windows" toegevoegd wordt aan CanvasHs, dan gebeurd het ontwikkelen van die code op de branch "dev/windows". Als "dev/windows" in een stabiele status is met documentatie en tests kan er een merge aangevraagd worden naar dev. Als er een release voorbereid wordt zal er vanuit dev weer naar master gemerged worden.

Wil je werken aan twee features tegelijk zul je twee branches moeten maken vanuit *dev*. Zo houden we code apart van elkaar, en houden we het duidelijk welke features waar gemaakt worden. Wil iemand anders meewerken aan jouw feature kan hij gewoon die branch checkouten.
