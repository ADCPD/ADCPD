<!-- Header Section -->
<h1 align="center">👋 Hi, I'm <strong>Amir Dhaouadi</strong></h1>
<h3 align="center">🚀 Lead Full-Stack Developer — Symfony, API Platform, Vue & React</h3>

<p align="center">
  <a href="https://github.com/ADCPD"><img src="https://img.shields.io/github/followers/ADCPD?label=Follow&style=social" alt="GitHub Followers"></a>
  <a href="https://www.linkedin.com/in/dhaouadiamir/"><img src="https://img.shields.io/badge/LinkedIn-Amir%20Dhaouadi-blue?style=flat&logo=linkedin"></a>
  <a href="https://twitter.com/adcpd"><img src="https://img.shields.io/badge/Twitter-@adcpd-blue?style=flat&logo=twitter"></a>
  <a href="mailto:dhaouadi.amir@gmail.com"><img src="https://img.shields.io/badge/Email-Contact%20Me-red?style=flat&logo=gmail"></a>
  <a href="#"><img src="https://img.shields.io/badge/Expérience-12 ans%20depuis%202013-4CAF50?style=flat&logo=clockify&logoColor=white" alt="Expérience depuis 2013"></a>
</p>

<p align="center">
      <a href="https://sensiolabs.com/fr"><img src="https://img.shields.io/badge/SensioLabs-Symfony%20Developer?style=for-the-badge&logo=symfony&logoColor=white" alt="Sensiolabs Followers"></a>
</p>

---

## 🧩 About me

```php
<?php

namespace App\Developer;

#[AsHuman]
final class AmirDHAOUADI extends LeadDeveloper implements FullStackEngineer, ScrumMaster
{
    use Symfony;
    use APIPlatform;
    use Vue3;
    use NuxtJs;
    use ReactJs;
    use NextJs;
    use Typescript;
    use StimulusJs;
    use Docker;
    use PostgreSQL;
    use MySQL;
    use AgileMindset;
    use Craftsmanship;
    use TTD;
    use DDD;

    public const LOCATION = 'Paris, France 🇫🇷';
    public const EMAIL = 'dhaouadi.amir@gmail.com';
    public const OPEN_FOR_FREELANCE = true;

    public function getCurrentMissions(): array
    {
        return [
            'SensioLabs' => [
                'since' => '2024-05',
                'role' => 'Lead developpeur Symfony - JS',
                'projects' => [
                    'Base de données publique des medicaments' => 'https://base-donnees-publique.medicaments.gouv.fr/',
                    'Groupama 𝑰𝑭𝑼𝑪' => '𝑰𝑭𝑼𝑪 𝑷𝒍𝒂𝒕𝒇𝒐𝒓𝒎 (𝑻𝒂𝒙 𝑷𝒓𝒆-𝑪𝒂𝒍𝒄𝒖𝒍𝒂𝒕𝒊𝒐𝒏 𝒇𝒐𝒓 𝑭𝒓𝒆𝒏𝒄𝒉 𝑻𝒂𝒙 𝑨𝒖𝒕𝒉𝒐𝒓𝒊𝒕𝒊𝒆𝒔) : Mise en place d’un framework interne basé sur Vue 3 et TypeScript, intégrant une bibliothèque de composants réutilisables destinée à l’ensemble du service MAPP.',
                    'Groupama GOI - PCG' => '𝑮𝑶𝑰/𝑷𝑪𝑮 (𝑰𝒏𝒔𝒖𝒓𝒂𝒏𝒄𝒆 & 𝑩𝒓𝒐𝒌𝒆𝒓𝒂𝒈𝒆 𝑷𝒍𝒂𝒕𝒇𝒐𝒓𝒎 𝒇𝒐𝒓 𝑶𝒗𝒆𝒓𝒔𝒆𝒂𝒔 𝑴𝒂𝒓𝒌𝒆𝒕𝒔)',
                    'Groupama 𝑮𝑭𝑨' => '𝑮𝑭𝑨 (𝑮𝒓𝒐𝒖𝒑𝒂𝒎𝒂 𝑭𝒐𝒓𝒆𝒔𝒕 𝑰𝒏𝒔𝒖𝒓𝒂𝒏𝒄𝒆)',
                    'Groupama Infra' => 'Migration d\'environnments de developpment à partir de PDT à WSL via Windows 11'
                     
                ]
            ],
            'SUEZ 3S Lab' => [
                'since' => '2022-10',
                'role' => 'Developer R&D - Portails Intelligents',
                'projects' => [
                    'Villagile' => 'https://www.suez.com/fr/villagile',
                    'Tous Mes Services Déchets' => 'https://www.toutsurmesservices.fr/Un-compteur-de-dechets-intelligent-et-connecte-pour-jeter-moins-et-trier-mieux',
                    'Tous Mes Services Eaux' => 'https://www.toutsurmesservices.fr/?page=4&filter_home%5Bregion%5D=116'
                ]
            ],
            'Highteckers' => [
                'since' => '2018-01',
                'role' => 'Consultant Full-Stack Symfony/JS & Scrum Master',
                'clients' => ['Suez', 'Sidexa', 'Econocom', 'Believe', 'Boursorama', 'GreenFlex - Total']
            ],
        ];
    }
}
