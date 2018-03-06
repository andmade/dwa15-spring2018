# Blade templates
If we continued down the path outlined in the previous note set, we'd create individual views for all of our book routes. The problem with this is you'd end up with repeat code as each view would include your doctype, the `<head>`, the `<header>` with the logo, the `<footer>`, etc.

A better solution is to divide your views into __layout templates__ and __child views__.

This is called __template inheritance__ and an example is conveyed in this graphic:

<img src='https://s3.amazonaws.com/making-the-internet/laravel-view-inheritance@2x.png' style='max-width:792px;' alt=''>

With template inheritance you create a __master layout__ view (figure a) that contains common, shared parts that similar HTML files/views will need. For example, the doctype, the `<head>`, CSS and JavaScript includes, menus, footers, etc. 

Then, you'll create __child__ views (figures b and c) for individual pages that __inherit__ the master template.

In the master layout, you'll define __sections__ and __stacks__ that act as placeholders to be filled in with content defined in the child views.


## Example
Let's apply template inheritance to our book example thus far and start by creating a new layout view at `/resources/views/layouts/master.blade.php` (note `layouts` is a new subdirectory).

In this new file, add these contents:

```html
<!doctype html>
<html>
<head>
    <title>@yield('title', 'Foobooks')</title>
    <meta charset='utf-8'>
    <link href='/css/foobooks.css' type='text/css' rel='stylesheet'>

    @stack('head')
</head>
<body>

<header>
    <a href='/'><img src='/images/foobooks-logo@2x.png' id='logo' alt='Foobooks Logo'></a>
</header>

<section>
    @yield('content')
</section>

<footer>
    &copy; {{ date('Y') }}
</footer>

<script src='https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js'></script>

@stack('body')

</body>
</html>
```

Note how everything in this view is pretty generic&mdash; it could be applied to any page of our Foobooks app thus far. Also note the use of Blade directives like `@yield` and `@stack`.

Next, we want to adapt `/resources/views/book/show.blade.php` into a child view so *replace* the content there with this code:

```html
@extends('layouts.master')

@section('title')
    {{ $title }}
@endsection

@push('head')
    {{-- Page specific CSS includes should be defined here; this .css file does not exist yet, but we can create it --}}
    <link href='/css/books/show.css' type='text/css' rel='stylesheet'>
@endpush

@section('content')
    <h1>{{ $title }}</h1>
    
    <p>
        Details about this book will go here...
    </p>
@endsection
```

Note how indentation is used to show the hierarchy of content in the Blade directives. For example, the body of the `@section('content`)` directed is all indented 1x.

Run `http://foobooks.loc/books/war-and-peace` in your browser and test everything is working as it did before we implemented template inheritance:

<img src='https://s3.amazonaws.com/making-the-internet/laravel-first-view-with-assets@2x.png' style='max-width:743px;' alt='First view with assets loaded'>


## External CSS/JS Includes
+ In the master template, the jQuery library was included just as an example of where you include any external JavaScript files. We won't actually be using jQuery in this project.
+ The master layout has a `@stack('head')` and `@stack('body')` which allows the child views to define external CSS and/or JS includes specific to that child view.
+ The `@stack('head')` is positioned where you'd typically find page-specific CSS includes&mdash; after global CSS includes and before the closing `</head>` tag.
+ The `@stack('body')` is positioned where you'd typically find page-specific JS includes&mdash; after global JS includes and before the closing `</body>` tag.
+ It's not required that child views always specify content for all sections and stacks. In the above child view example (`show.blade.php`) you can see that content for the `@stack('body')` is never defined.




