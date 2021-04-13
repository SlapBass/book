# Die Roest Programmeringstaal

[Die Roest Programmeringstaal](title-page.md)

[Voorwoord](foreword.md)

[Inleiding](ch00-00-introduction.md)

## Aan die gang kom

- [Aan die gang kom](ch01-00-getting-started.md)

    - [Installasie](ch01-01-installation.md)
    - [Hello Wêreld!](ch01-02-hello-world.md)
    - [Hallo, vrag!](ch01-03-hello-cargo.md)

- [Programmering van 'n raai-speletjie](ch02-00-guessing-game-tutorial.md)

- [Algemene programmeringskonsepte](ch03-00-common-programming-concepts.md)

    - [Veranderlikes en veranderlikheid](ch03-01-variables-and-mutability.md)
    - [Datatipes](ch03-02-data-types.md)
    - [Funksies](ch03-03-how-functions-work.md)
    - [Opmerkings](ch03-04-comments.md)
    - [Beheer vloei](ch03-05-control-flow.md)

- [Begrip van eienaarskap](ch04-00-understanding-ownership.md)

    - [Wat is eienaarskap?](ch04-01-what-is-ownership.md)
    - [Verwysings en leen](ch04-02-references-and-borrowing.md)
    - [Die snytipe](ch04-03-slices.md)

- [Die gebruik van structs om verwante data te struktureer](ch05-00-structs.md)

    - [Omskrywing en instelling van strukture](ch05-01-defining-structs.md)
    - ['N Voorbeeldprogram wat Structs gebruik](ch05-02-example-structs.md)
    - [Metodesintaksis](ch05-03-method-syntax.md)

- [Enums en patroonpassing](ch06-00-enums.md)

    - [Definisie van 'n Enum](ch06-01-defining-an-enum.md)
    - [Die `match` Control Flow Operator](ch06-02-match.md)
    - [Beknopte beheervloei met `if let`](ch06-03-if-let.md)

## Basiese roesgeletterdheid

- [Groeiprojekte met pakkette, kratte en modules bestuur](ch07-00-managing-growing-projects-with-packages-crates-and-modules.md)

    - [Pakkies en kratte](ch07-01-packages-and-crates.md)
    - [Definiëring van modules om die omvang en privaatheid te beheer](ch07-02-defining-modules-to-control-scope-and-privacy.md)
    - [Paaie om na 'n item in die moduleboom te verwys](ch07-03-paths-for-referring-to-an-item-in-the-module-tree.md)
    - [Om paaie te omvang met die `use` sleutelwoord](ch07-04-bringing-paths-into-scope-with-the-use-keyword.md)
    - [Skei modules in verskillende lêers](ch07-05-separating-modules-into-different-files.md)

- [Algemene versamelings](ch08-00-common-collections.md)

    - [Stoor lyste van waardes by vektore](ch08-01-vectors.md)
    - [Stoor UTF-8-gekodeerde teks met snare](ch08-02-strings.md)
    - [Stoor sleutels met gepaardgaande waardes in Hash Maps](ch08-03-hash-maps.md)

- [Fouthantering](ch09-00-error-handling.md)

    - [Onherstelbare foute met `panic!`](ch09-01-unrecoverable-errors-with-panic.md)
    - [Herstelbare foute met `Result`](ch09-02-recoverable-errors-with-result.md)
    - [Om `panic!` of nie om `panic!`](ch09-03-to-panic-or-not-to-panic.md)

- [Generiese tipes, eienskappe en leeftye](ch10-00-generics.md)

    - [Generiese datatipes](ch10-01-syntax.md)
    - [Eienskappe: Definiëring van gedeelde gedrag](ch10-02-traits.md)
    - [Verifiëring van verwysings met leeftye](ch10-03-lifetime-syntax.md)

- [Skryf van outomatiese toetse](ch11-00-testing.md)

    - [Hoe om toetse te skryf](ch11-01-writing-tests.md)
    - [Beheer hoe toetse uitgevoer word](ch11-02-running-tests.md)
    - [Toetsorganisasie](ch11-03-test-organization.md)

- ['N I / O-projek: die opstel van 'n opdraglynprogram](ch12-00-an-io-project.md)

    - [Aanvaarding van bevelreëlargumente](ch12-01-accepting-command-line-arguments.md)
    - [Lees 'n lêer](ch12-02-reading-a-file.md)
    - [Refactoring om die modulariteit en fouthantering te verbeter](ch12-03-improving-error-handling-and-modularity.md)
    - [Die ontwikkeling van die biblioteek se funksionaliteit met toetsgedrewe ontwikkeling](ch12-04-testing-the-librarys-functionality.md)
    - [Werk met omgewingsveranderlikes](ch12-05-working-with-environment-variables.md)
    - [Skryf van foutboodskappe na standaardfout in plaas van standaarduitsette](ch12-06-writing-to-stderr-instead-of-stdout.md)

## Dink in Rust

- [Funksionele taalkenmerke: wisselvorme en sluitings](ch13-00-functional-features.md)

    - [Sluitings: anonieme funksies wat hul omgewing kan vasvang](ch13-01-closures.md)
    - [Verwerking van 'n reeks artikels met Iterators](ch13-02-iterators.md)
    - [Ons I / O-projek verbeter](ch13-03-improving-our-io-project.md)
    - [Vergelyking van prestasie: Loops vs Iterators](ch13-04-performance.md)

- [Meer oor Cargo en Crates.io](ch14-00-more-about-cargo.md)

    - [Aanpassing van geboue met vrystellingsprofiele](ch14-01-release-profiles.md)
    - [Publiseer 'n krat na Crates.io](ch14-02-publishing-to-crates-io.md)
    - [Vragwerkspasies](ch14-03-cargo-workspaces.md)
    - [Binaries installering van Crates.io met `cargo install`](ch14-04-installing-binaries.md)
    - [Vrag uit te brei met aangepaste opdragte](ch14-05-extending-cargo.md)

- [Slim aanwysers](ch15-00-smart-pointers.md)

    - [Gebruik `Box<T>` om na data op die hoop te wys](ch15-01-box.md)
    - [Die hantering van slim wenke soos gereelde verwysings met die `Deref` eienskap](ch15-02-deref.md)
    - [Running Code vir skoonmaak met die `Drop` Trait](ch15-03-drop.md)
    - [`Rc<T>` , die verwysingsgetelde slimwyser](ch15-04-rc.md)
    - [`RefCell<T>` en die binne-veranderbaarheidspatroon](ch15-05-interior-mutability.md)
    - [Verwysingsiklusse kan geheue lek](ch15-06-reference-cycles.md)

- [Vreeslose gelyktydigheid](ch16-00-concurrency.md)

    - [Gebruik drade om kode gelyktydig uit te voer](ch16-01-threads.md)
    - [Gebruik die boodskap deurgee om data tussen die draadjies oor te dra](ch16-02-message-passing.md)
    - [Gedeelde-staat-gelyktydigheid](ch16-03-shared-state.md)
    - [Uitbreidbare gelyktydigheid met die eienskappe van `Sync` en `Send`](ch16-04-extensible-concurrency-sync-and-send.md)

- [Voorwerpgerigte programmeringseienskappe van roes](ch17-00-oop.md)

    - [Eienskappe van objekgerigte tale](ch17-01-what-is-oo.md)
    - [Gebruik eienskappe van waardes van verskillende soorte](ch17-02-trait-objects.md)
    - [Implementering van 'n objekgerigte ontwerppatroon](ch17-03-oo-design-patterns.md)

## Gevorderde onderwerpe

- [Patrone en bypassing](ch18-00-patterns.md)

    - [Al die plekke se patrone kan gebruik word](ch18-01-all-the-places-for-patterns.md)
    - [Weerlegbaarheid: of 'n patroon miskien nie ooreenstem nie](ch18-02-refutability.md)
    - [Patroon Sintaksis](ch18-03-pattern-syntax.md)

- [Gevorderde funksies](ch19-00-advanced-features.md)

    - [Onveilige Roes](ch19-01-unsafe-rust.md)
    - [Gevorderde eienskappe](ch19-03-advanced-traits.md)
    - [Gevorderde tipes](ch19-04-advanced-types.md)
    - [Gevorderde funksies en sluitings](ch19-05-advanced-functions-and-closures.md)
    - [Makro's](ch19-06-macros.md)

- [Finale projek: die bou van 'n multidraad-bediener](ch20-00-final-project-a-web-server.md)

    - [Die bou van 'n enkelbediener webbediener](ch20-01-single-threaded.md)
    - [Omskep van ons enkelbedraad-bediener in 'n meervoudige bediener](ch20-02-multithreaded.md)
    - [Grasieuse afskakeling en opruiming](ch20-03-graceful-shutdown-and-cleanup.md)

- [Aanhangsel](appendix-00.md)

    - [A - Sleutelwoorde](appendix-01-keywords.md)
    - [B - Operateurs en simbole](appendix-02-operators.md)
    - [C - Afleibare eienskappe](appendix-03-derivable-traits.md)
    - [D - Nuttige ontwikkelingsinstrumente](appendix-04-useful-development-tools.md)
    - [E - uitgawes](appendix-05-editions.md)
    - [F - Vertalings van die boek](appendix-06-translation.md)
    - [G - Hoe word roes gemaak en 'n nagroes '](appendix-07-nightly-rust.md)
