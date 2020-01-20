# Projekt zaliczeniowy kursu "Usługi i platformy deweloperskie dla aplikacji w Chmurze"

### Wykorzystywane usługi Azure
- Azure Cosmos DB
- App Services

### Wymagane narzędzia do wdrożenia projektu:
- [Git](https://git-scm.com/)

## Konfigurowanie usługi Azure Cosmos DB

Z poziomu portalu Microsoft Azure należy wyszukać usługę **Azure Cosmos DB**, a następnie rozpocząć proces dodawania nowej usługi.

![Lista zasobów Azure Cosmos DB](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/01-cosmos-db-create-resource-list.png "Lista zasobów Azure Cosmos DB")

Na formularzu służącym do tworzenia nowej usługi wybieramy Resource Group (lub tworzymy nową jeśli jej nie posiadamy), wypełniamy pole *Account Name* wpisując nową nazwę konta dla naszego serwisu. Z listy API wybieramy *Azure Cosmos DB for MongoDB API*. Jako region wybieramy Europę. Pozostałe ustawienia zostawiamy domyślne. Następnie klikamy przycisk *Review + create*.

![Tworzenie nowego zasobu Azure Cosmos DB](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/02-cosmos-db-create-resource-form.png "Tworzenie nowego zasobu Azure Cosmos DB")

Gdy wyświetli nam się pomyślny komunikat walidacji klikamy przycisk *Create*.

![Podsumowanie tworzenia nowego zasobu Azure Cosmos DB](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/03-cosmos-db-create-resource-review.png "Podsumowanie tworzenia nowego zasobu Azure Cosmos DB")

## Konfigurowanie usługi AppServices ##

Z poziomu portalu Microsoft Azure należy wyszukać usługę **App Services**, a następnie rozpocząć proces dodawania nowej usługi.

![Lista zasobów App Services](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/04-app-service-create-resource-list.png "Lista zasobów App Services")

Na formularzu służącym do tworzenia nowej usługi wybieramy Resource Group (lub tworzymy nową jeśli jej nie posiadamy), wypełniamy pole *Name* nazwą naszej nowej aplikacji. Z listy Runtime stack wybieramy *Node 10 LTS*. Jako region wybieramy Europę. Pozostałe ustawienia zostawiamy domyślne. Następnie klikamy przycisk *Review + create*.

![Tworzenie nowego zasobu App Services](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/05-app-service-create-resource-form.png "Tworzenie nowego zasobu App Services")

Gdy wyświetli nam się pomyślny komunikat walidacji klikamy przycisk *Create*.

![Podsumowanie tworzenia nowego zasobu App Services](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/06-app-service-create-resource-review.png "Podsumowanie tworzenia nowego zasobu App Services")

Po wdrożeniu usługi przechodzimy do nowo utworzonego zasobu. Z menu wybieramy **Deployment/Deployment Center** a następnie jako metodę wdrażania wybieramy *Local Git*.

![Wybór sposobu wdrażania - source control](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/07-deployment-center-source-control.png "Wybór sposobu wdrażania - source control")

Jako Build Provider wybieramy *App Service build service*.

![Wybór sposobu wdrażania - build provider](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/08-deployment-center-build-provider.png "Wybór sposobu wdrażania - build provider")

Na końcu klikamy przycisk *Finish*.

![Wybór sposobu wdrażania - podsumowanie](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/09-deployment-center-summary.png "Wybór sposobu wdrażania - podsumowanie")

## Wdrożenie aplikacji

Aby wdrożyć alikację musimy ją najpierw pobrać używając polecenia

```shell
git clone https://github.com/pdyplomowa/azure-project-prod.git
```
Następnie przechodzimy do naszego nowo utworzonego zasobu usługi Azure Cosmos DB i wybieramy z menu **Settings/Connection String**.

![Azure Cosmos DB Connection String](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/10-connection-string.png "Azure Cosmos DB Connection String")

Z tego menu przeklejamy wartości do pliku *environment.js* w naszym projekcie.

| environment.js | Connection string |
| -------------- | ----------------- |
| accountName    | USERNAME          |
| databaseName   | 'admin'           |
| password       | PRIMARY PASSWORD  |
| port           | PORT              |

![environment.js](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/11-environmentjs.png "environment.js")

Na koniec wykonujemy komende

```shell
git commit -am "db credentials"
```

![Git commit environment.js](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/12-commit-enviromentjs.png "Git commit environment.js")

Po wypełnieniu wartości w pliku *environment.js* przechodzimy do naszego zasobu App Service w Azure i w menu wybieramy **Deployment/ Deployment Center**

![Deployment Center menu](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/13-deployment-center-menu.png "Deployment Center menu")

 Kopiujemy *Git Clone Url* i w lokalizacji naszego projektu wykonujemy polecenie 
 
 ```shell
 git remote add azure <git_clone_url>
 ```
 ![Dodawanie deployment remote](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/14-git-add-remote.png "Dodawanie deployment remote")
 
 Po czym następnie wykonujemy komendę
 
 ```shell
 git push azure master
 ```
 
 logując się za pomocą Deployment Credentials, które znajdują się pod przyciskiem powyżej Git Clone Url w Azure
 
 ![Deployment credentials](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/15-deployment-credentials.png "Deployment credentials")
 
 ![Git push](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/16-git-push-with-credentials.png "Git push")
 
 Na koniec powinniśmy dostać informację o poprawnym wdrożeniu aplikacji. Gdy klikniemy przycisk Browse w Azure będziemy w stanie korzystać z aplikacji
 
 ![Pomyślne wdrożenie](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/17-successful-deployment.png "Pomyślne wdrożenie")
 
 ![Deployment center browse](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/18-deployment-center-browse.png "Deployment center browse")
 
 ![Widok aplikacji](https://github.com/pdyplomowa/azure-project-prod/blob/master/screenshots/19-application.png "Widok aplikacji")
