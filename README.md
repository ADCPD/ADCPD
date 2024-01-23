🔥 Hi 🔥 

````php
<?php

namespace App\Developer;

#[AsHuman]
final class AmirDHAOUADI extends SymfonyDeveloper implements FontEndDeveloper
{
    use Symfony;
    use PostgreSQL;
    use MySQL;
    use Twig;
    use JQuery;
    use ReactJs;
    use NextJs;
    use Docker;

    use Ops;

    use Po;
    use ScrumMaster;

    public const FIRST_NAME = 'Amir';
    public const LAST_NAME = 'DHAOUADI';
    
    public function __construct(
        private \DateTimeImmutable $birthDate = new \DateTimeImmutable('1988-06-24'),
        private string $email = 'dhaouadi.amir@gmail.com',
        private array $currentCompanies = [
            'SUEZ 3S Lab'  => [
                'since'           => '10-2022',
                'responsibility'  => 'Developer R&D',
                'project'         => [
                    "Portail Villagile : https://www.suez.com/fr/villagile",
                    "Portail Tous mes services dechets : https://www.toutsurmesservices.fr/Un-compteur-de-dechets-intelligent-et-connecte-pour-jeter-moins-et-trier-mieux",
                    "Portail Tous mes services eaux : https://www.toutsurmesservices.fr/?page=4&filter_home%5Bregion%5D=116",
                ]
             ],
            'Highteckers' => [
                'since'           => '01-2018',
                'responsibility'  => 'Consultant : Full-stack Web Developer Symfony Js + Scrum Master',
                'company'         => [
                    'Suez',
                    'Sidexa',
                    'Econocom',
                    'Believe',
                    'Boursorama',
                    'GreenFlex - Total'
                ];
            ],
        ],
        private string $currentCity = 'Paris, France';
    ) {}
    
    public function getTwitter(): ?SocialAccountInterface
    {
        return new TwitterAccount('[https://twitter.com/oskarstark](https://twitter.com/adcpd)](https://twitter.com/adcpd)');
    }

    public function getLinkedIn(): ?SocialAccountInterface
    {
        return new TwitterAccount('[https://www.linkedin.com/in/dhaouadiamir](https://www.linkedin.com/in/dhaouadiamir)');
    }
    
    public function isOpenForFreelanceWork(): bool
    {
        return true;
    }

    public function isOpenForCDI(): bool
    {
        return false;
    }
}
````
