# ConsumindoApi

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 10.1.0.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).



# Steps to read a api:

1 - [METHOD]
    create a method in app/services/
    ng g s services/crud
    
  constructor(private http: HttpClient) { }
  public getFotos():Observable<any> {
    return this.http.get(`https://jsonplaceholder.typicode.com/photos`)
  } 

  //method GET to url from image that be import
  // Here's the Magic!

2 - [MODELS]
    Copy code json from api, create a model and format to:

export class Images {
    public albumId: number;
    public id: number;
    public title: string;
    public url: string;
    public thumbnailUrl: string;
}


3 - [COMPONENT]
    ng g c componentes/crud
    lets add on crud-component.ts:


export class CrudComponent implements OnInit {
images: Images;
erro: any;
  constructor(private crudService: CrudService) { 
    this.getter();
  }

  //lifecycle
  ngOnInit(): void { 
  }
  getter() {
    this.crudService.getFotos().subscribe((data: Images) => {
      this.images = data;
      console.log('Recebemos : ', data);
      console.log('A variavel que prenchemos: ', this.images)
    }, (error: any) => {
      this.erro = error;
      console.error("ERROR: ", error);
    })
  }

}


4 - [ROUTE]
    into app.module.ts
  
        import:
      HttpClientModule
  
  providers: [HttpClient],


5 - [VIEW]
    Into crud.component.html

    <div *ngFor="let i of images">
	<h1>{{ i.title }}</h1>
	<img [attr.src]=" i.url " />
    </div>




    Into app.component.html

    <app-crud></app-crud>


