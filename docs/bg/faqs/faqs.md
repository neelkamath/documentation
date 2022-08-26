# Често задавани въпроси

## Какво е SubQuery?

SubQuery представлява блокчейн индексатор на данни с отворен код за разработчици, който предоставя бързи, гъвкави, надеждни и децентрализирани API за управление на водещи мулти-чейн приложения.

Нашата цел е да спестим време и пари на разработчиците, като елиминираме необходимостта от изграждане на собствено решение за индексиране. Затова, те ще могат напълно да се съсредоточат върху разработването на своите приложения. SubQuery помага на разработчиците да създават децентрализираните продукти от бъдещето.

<figure class="video_container">
<iframe src="https://www.youtube.com/embed/gCpVz_mkWdo" title="Представяне на SubQuery Network" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscree="true"></iframe>
</figure>

**Управлявана услуга на SubQuery**

SubQuery also provides free, production grade hosting of projects for developers. Our Managed Service removes the responsiblity of managing infrastructure, so that developers do what they do best — build. Find out more [here](/run_publish/publish.md).

**Мрежата на SubQuery**

The SubQuery Network allows developers to completely decentralise their infrastructure stack. It is the most open, performant, reliable, and scalable data service for dApps. The SubQuery Network indexes and services data to the global community in an incentivised and verifiable way.  After publishing your project to the SubQuery Network, anyone can index and host it - providing data to users around the world faster and reliably.

More information [here](/subquery_network/introduction.md).

## Кой е най-добрият начин да стартирате работа със SubQuery?

The best way to get started with SubQuery is to try out our [Hello World tutorial](/assets/pdf/Hello_World_Lab.pdf). This is a simple 5 min walk through exercise. Download the starter template, build the project, use Docker to run a node on your localhost, and run a simple query.

## По какъв начин мога да допринеса или да дам обратна връзка към SubQuery?

Ние харесваме приноса и обратната връзка от общността. To contribute the code, fork the repository of your interest and make your changes. След това изпратете PR или Pull Request. Don't forget to test as well. Also check out our <a href="http://localhost:8080/miscellaneous/contributing.html">contributions guidelines.</a>

За да дадете обратна връзка, свържете се с нас на hello@subquery.network или преминете към нашия [канал на discord](https://discord.com/invite/78zg8aBSMG).

## Колко струва хостването на моя проект в SubQuery Projects?

This service is being provided to the community with a generous free tier! You can host your first two SubQuery projects for absolutely free!

## Какво представляват слотовете за разполагане?

Слотовете за внедряване са функция в [SubQuery Projects](https://project.subquery.network), която е еквивалент на среда за разработка. Например, във всяка софтуерна организация обикновено има среда за разработка и среда за производство като минимум (игнорирайки localhost). Обикновено се включват допълнителни среди, като сценична и предварителна продукция или дори QA, в зависимост от нуждите на организацията и нейната настройка за развитие.

В момента SubQuery има два налични слота. Слот за подготовка и слот за производство. Това позволява на разработчиците да разположат своите SubQuery в промежутъчната среда и всичко да върви добре, да се „повишат до производство“ с едно натискане на бутон.

## Какво е предимството на етапния слот?

Основното предимство от използването на етапен слот е, че ви позволява да подготвите ново издание на вашия проект SubQuery, без да го излагате публично. Можете да изчакате междинният слот да преиндексира всички данни, без това да повлияе на производствените ви приложения.

Промежутъчният слот не се показва публично в [Explorer](https://explorer.subquery.network/) и има уникален URL адрес, който се вижда само от вас. И разбира се, отделната среда ви позволява да тествате новия си код, без да засягате производството.

## Какви са външните характеристики на Polkadot?

Ако вече сте запознати с блокчейн концепциите, можете да мислите за външните елементи като сравними с транзакциите. По-формално обаче, външната е част от информацията, която идва извън веригата и е включена в блок. Има три категории външни елементи. Те са присъщи, подписани транзакции и неподписани транзакции.

Присъщите външни елементи са части от информация, които не са подписани и са вмъкнати в блок само от автора на блока.

Подписани външни транзакции са транзакции, които съдържат подпис на акаунта, който е издал транзакцията. Те трябва да платят такса, за да бъде включена транзакцията във веригата.

Външни неподписани транзакции са транзакции, които не съдържат подпис на акаунта, който е издал транзакцията. Неподписаните външни транзакции трябва да се използват внимателно, защото никой не плаща такса, защото те не са подписани. Поради това на опашката за транзакции липсва икономическа логика за предотвратяване на спам.

За повече информация щракнете [тук](https://substrate.dev/docs/en/knowledgebase/learn-substrate/extrinsics).

## Каква е крайната точка за мрежата Kusama?

Network.endpoint за мрежата Kusama е `wss://kusama.api.onfinality.io/public-ws`.

## Каква е крайната точка за основната мрежа на Polkadot?

Network.endpoint за мрежата Polkadot е `wss://polkadot.api.onfinality.io/public-ws`.

## Как да разработя итеративно моята проектна схема?

Известен проблем при разработването на променяща се схема на проект е, че при стартиране на вашия възел на подзаявка за тестване, индексираните по-рано блокове ще бъдат несъвместими с новата ви схема. За да се разработят итеративно схеми, индексираните блокове, съхранени в базата данни, трябва да бъдат изчистени, това може да се постигне чрез стартиране на вашия възел с флага `--force-clean`. Например:

```shell
subql-node -f . --force-clean --subquery-name=<project-name>
```

Обърнете внимание, че се препоръчва да използвате `--force-clean`, когато променяте `startBlock` в манифеста на проекта (`project.yaml`), за да започнете преиндексиране от конфигурирания блок. If `startBlock` is changed without a `--force-clean` of the project, then the indexer will continue indexing with the previously configured `startBlock`.


## How can I optimise my project to speed it up?

Performance is a crucial factor in each project. Fortunately, there are several things you could do to improve it. Here is the list of some suggestions:

- Avoid using block handlers where possible.
- Query only necessary fields.
- Try to use filter conditions to reduce the response size. Create filters as specific as possible to avoid querying unnecessary data.
- For large data tables, avoid querying `totalCount` without adding conditions.
- Add indexes to entity fields for query performance, this is especially important for historical projects.
- Set the start block to when the contract was initialised.
- Always use a [dictionary](../tutorials_examples/dictionary.html#how-does-a-subquery-dictionary-work) (we can help create one for your new network).
- Optimise your schema design, keep it as simple as possible.
    - Try to reduce unnecessary fields and columns.
    - Create  indexes as needed.
- Use parallel/batch processing as often as possible.
    - Use `api.queryMulti()` to optimise Polkadot API calls inside mapping functions and query them in parallel. This is a faster way than a loop.
    - Use `Promise.all()`. In case of multiple async functions, it is better to execute them and resolve in parallel.
    - If you want to create a lot of entities within a single handler, you can use `store.bulkCreate(entityName: string, entities: Entity[])`. You can create them in parallel, no need to do this one by one.
- Making API calls to query state can be slow. You could try to minimise calls where possible and to use `extrinsic/transaction/event` data.
- Use `worker threads` to move block fetching and block processing into its own worker thread. It could speed up indexing by up to 4 times (depending on the particular project). You can easily enable it using the `-workers=<number>` flag. Note that the number of available CPU cores strictly limits the usage of worker threads. For now, it is only available for Substrate and Cosmos and will soon be integrated for Avalanche.
- Note that `JSON.stringify` doesn’t support native `BigInts`. Our logging library will do this internally if you attempt to log an object. We are looking at a workaround for this.
- Use a convenient `modulo` filter to run a handler only once to a specific block. This filter allows handling any given number of blocks, which is extremely useful for grouping and calculating data at a set interval. For instance, if modulo is set to 50, the block handler will run on every 50 blocks. It provides even more control over indexing data to developers and can be implemented like so below in your project manifest.