# Хостване на проект с помощта на IPFS

Това ръководство ще ви преведе през това как да публикувате локален проект SubQuery в [IPFS](https://ipfs.io/) и да го разположите в нашата хостинг инфраструктура.

Хостването на проект в IPFS го прави достъпен за всички и намалява зависимостта ви от централизирани услуги като GitHub.

## Изисквания

- `@subql/cli` версия 0.21.0 или по-нова.
- Manifest `specVersion` 1.0.0 and above.
- Get your [SUBQL_ACCESS_TOKEN](ipfs.md#prepare-your-subql-access-token) ready.
- За да сте сигурни, че внедряването ви е успешно, силно препоръчваме да изградите проекта си с командата `subql build` и да го тествате локално, преди да го публикувате.

## Подгответе своя SUBQL_ACCESS_TOKEN

- Стъпка 1: Отидете на [SubQuery Projects](https://project.subquery.network/) и влезте.
- Стъпка 2: Кликнете върху вашия профил в горния десен ъгъл на навигационното меню, след което щракнете върху **_Опресняване на токена_**.
- Стъпка 3: Копирайте генерирания токен.
- Стъпка 4: За да използвате този токен:
  - Вариант 1: Добавете SUBQL_ACCESS_TOKEN в променливите на вашата среда. `EXPORT SUBQL_ACCESS_TOKEN=<token>` (Windows) or `export SUBQL_ACCESS_TOKEN=<token>` (Mac/Linux)
  - Опция 2: Очаквайте скоро, `subql/cli` ще поддържа локално съхранение на вашия SUBQL_ACCESS_TOKEN.

## Как да публикувате проект

Предлагаме два метода за публикуване на вашия проект:

### Опция 1

Тъй като вече сте инсталирали `@subql/cli`, можете да изпълните следната команда, която ще прочете проекта и необходимата информация от неговия манифест по подразбиране `project.yaml`:

```
// Publish it from your project's root directory
subql publish

// OR point to your project root
subql publish -f ~/my-project/
```

### Опция 2

Като алтернатива, да предположим, че вашият проект има множество манифестни файлове, например поддържате множество мрежи, но споделяте един и същ мапинг и бизнес логика и имате структура на проекта, както следва:

```
L projectRoot
 L src/
 L package.json
 L polkadot.yaml (Manifest for Polkadot network)
 L kusama.yaml   (Manifest for Kusama network)
 ...
```

Винаги можете да публикувате проекта с избрания от вас манифест файл.

```
 # This will publish project support indexing Polkadot network
subql publish -f ~/my-projectRoot/polkadot.yaml
```

## След публикуване

След успешното публикуване на проекта, логовете по-долу показват, че проектът е създаден в IPFS клъстера и са върнали неговия `CID` (идентификатор на съдържанието).

```
Building and packing code... done
Uploading SupQuery project to IPFS
SubQuery Project uploaded to IPFS: QmZ3q7YZSmhwBiot4PQCK3c7Z6HkteswN2Py58gkkZ8kNd  //CID
```

Моля, обърнете внимание на този `CID`. With this `CID`, you can view your published project as what we call it [IPFS Deployment](ipfs.md#ipfs-deployment).

With `@subql/cli` version 1.3.0 or above, when using `subql publish` it will store a copy of the project's `IPFS CID` in a file in your project directory, the naming of the file will be consistent with your project.yaml. For example, if your manfiest file is named `project.yaml`, the IPFS file will be named  `.project-cid`.

## IPFS Deployment

IPFS deployment представлява независимо и уникално съществуване на проект SubQuery в децентрализирана мрежа. Следователно всякакви промени в кода в проекта ще повлияят на неговата уникалност. Ако трябва да коригирате вашата бизнес логика, напр. промените функцията за картографиране, трябва да публикувате отново проекта и `CID` ще се промени.

Засега, за да видите проекта, който сте публикували, използвайте `REST` API инструмент като [Postman](https://web.postman.co/) и използвайте метода `POST` със следния примерен URL за да го извлечете:`https://ipfs.subquery.network/ipfs/api/v0/cat?arg=<YOUR_PROJECT_CID>`.

Трябва да видите примерното внедряване на проекта, както е показано по-долу.

Това внедряване изглежда много подобно на вашия манифест файл. Можете да очаквате тези описателни полета и ендпойнта на мрежата и речника да са премахнати, тъй като не влияят пряко върху резултата от изпълнението на проекта.

Тези файлове, използвани във вашия локален проект, също са опаковани и публикувани в IPFS.

```yaml
dataSources:
  - kind: substrate/Runtime
    mapping:
      file: ipfs://QmTTJKrMVzCZqmRCd5xKHbKymtQQnHZierBMHLtHHGyjLy
      handlers:
        - handler: handleBlock
          kind: substrate/BlockHandler
        - filter:
            method: Deposit
            module: balances
          handler: handleEvent
          kind: substrate/EventHandler
        - handler: handleCall
          kind: substrate/CallHandler
    startBlock: 8973820
network:
  genesisHash: "0x91b171bb158e2d3848fa23a9f1c25182fb8e20313b2c1eb49219da7a70ce90c3"
schema:
  file: ipfs://QmTP5BjtxETVqvU4MkRxmgf8NbceB17WtydS6oQeHBCyjz
specVersion: 0.2.0
```

## Изпълнете своя проект SubQuery на хоствана услуга

### Създайте проект с IPFS внедряване

You can follow the guide to [Publish your SubQuery project](../run_publish/publish.md) but where you set your deployment source you can select **IPFS**.

След това изберете вашия производствен слот, копирайте и поставете своя CID за разгръщане на IPFS (без водещия `ipfs://`).

Трябва да видите внедряването на IPFS в секцията за предварителен преглед. И можете да изберете мрежата, ендпойнта на речника и т. н.

След успешно разгръщане на IPFS внедряването на нашата хоствана услуга, тя трябва да бъде достъпна за преглед в SubQuery Explorer, можете да получите достъп до услугата за заявки точно както правите локално.
