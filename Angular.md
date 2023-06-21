# Angular Notes

#### Loop
<pre class="notranslate">
<code>
<p> \*<li *ngFor="let person of people"> (1)
    {{ person.name }}
  </li>*/</p>
  </code></pre>
 ## Angular provides two different approaches to handling user input through forms: reactive and template-driven
 https://angular.io/guide/forms-overview
 
 what are pipes in Angular
 Ref: https://blog.bitsrc.io/pipes-in-angular-4f979af63dd7
 
Built-in pipes in Angular
Angular comes with many built-in pipes. Some of them include:

<div>
uppercase (to convert string in upper case)
lowercase (to convert string in upper case)
date (to format the date into different types)
json (to convert a value or object into JSON formatted string)
 
Examples of pipes in use:
<pre><code>
<p>{{ 'Makesh' | uppercase }}</p>
<p>{{ 'Kumar' | lowercase }}</p>
 <p>{{ { name: 'makesh' } | json }}</p></pre></code>
</div>
