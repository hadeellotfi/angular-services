# Angular Service Injection

Alternative Injection Syntax
Injecting services (or, in general: dependencies) into components via the constructor functions is the most common way of performing such injections. You'll see this approach in most Angular projects you'll be working on.
However, there also is an alternative way of injecting dependencies: Via Angular's inject() function.
Instead of injecting LoggingService like this:

```ts
	@Component(...)
	export class AccountComponent {
	  // @Input() & @Output() code as shown in the previous lecture
	 
	  constructor(private loggingService: LoggingService) {}
	}
```

you could inject it like this, by using the inject() function:
```ts
	import { Component, Input, Output, inject } from '@angular/core'; // <- Add inject import
	 
	@Component(...)
	export class AccountComponent {
	  // @Input() & @Output() code as shown in the previous lecture
	  private loggingService?: LoggingService; // <- must be added
	 
	  constructor () {
	    this. loggingService = inject(LoggingService);
	  }
	}
```

It's totally up to you which approach you prefer. In this course (and, as mentioned, in most projects), we'll use the constructor approach.

# # A Different Way Of Injecting Services

If you're using Angular 6+ (check your package.json  to find out), you can provide application-wide services in a different way.
Instead of adding a service class to the providers[]  array in AppModule , you can set the following config in @Injectable() :

```ts
1.	@Injectable({providedIn: 'root'})
2.	export class MyService { ... }
```
```ts
This is exactly the same as:
```
```ts
1.	export class MyService { ... }
```
and
```ts
1.	import { MyService } from './path/to/my.service';
2.	 
3.	@NgModule({
4.	    ...
5.	    providers: [MyService]
6.	})
7.	export class AppModule { ... }
```

Using this syntax is completely optional, the traditional syntax (using providers[] ) will also work.
The "new syntax" does offer one advantage though: Services can be loaded lazily by Angular (behind the scenes) and redundant code can be removed automatically.
 This can lead to a better performance and loading speed - though this really only kicks in for bigger services and apps in general.
