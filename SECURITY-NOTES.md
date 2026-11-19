# Notes de sécurité – TP7

**Q3.** `@main` est une branche mobile : le code de l'action peut changer sans prévenir (risque de chaîne d'approvisionnement) et le workflow n'est plus reproductible. Un tag `@v4` fige une version majeure. L'idéal est d'épingler un SHA de commit.

**Q4.** Non. Le badge prouve l'identité du publisher, pas la qualité ni l'absence de faille du code ; un compte peut être compromis et une action vérifiée peut contenir un bug.

**Q5.** (1) Lire le code source de l'action (action.yml, scripts) pour voir ce qu'elle fait avec les secrets et le réseau. (2) Vérifier la fiabilité du mainteneur (activité, étoiles, issues) et épingler un SHA de commit.