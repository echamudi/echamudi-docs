# Angular
## Accessing component properties from browser console
```js
ng.probe($$(`component-selector`)).componentInstance
```
## Accessing DOM element data from other DOM element.
```html
<input #phone placeholder="phone number">
<!-- phone refers to the input element --> 
<button (click)="callPhone(phone.value)">Call</button>
```
## Accessing component element data from other TS element.
Sub Component
```ts
@Component({
  selector: 'sub-component',
})
export class SubComponent {
   name = 'Angular';
}
```

Parent Component
```ts
@Component({
  selector: 'parent-component',
})
export class ParentComponent {
    @ViewChild('subComponent') subComponent: any;

}
```
```html
<sub-component #subComponent></app-hello>
```
