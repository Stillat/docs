# Sorting

- [Introduction](#intro)

<a name="intro"></a>
## Introduction

Stillat provides a convenient way to use different sorting algorithms within your application. At the current time, Stillat supports the following sorting algorithms (fully-qualified names are in parenthesis):

* Bogo (`\Stillat\Common\Collections\Sorting\BogoSorter`)
* Bubble (`\Stillat\Common\Collections\Sorting\BubbleSorter`)
* Cocktail (`\Stillat\Common\Collections\Sorting\CocktailSorter`)
* Gnome (`\Stillat\Common\Collections\Sorting\GnomeSorter`)
* Heap (`\Stillat\Common\Collections\Sorting\HeapSorter`)
* Insertion (`\Stillat\Common\Collections\Sorting\InsertionSorter`)
* Merge (`\Stillat\Common\Collections\Sorting\MergeSorter`)
* Quick (`\Stillat\Common\Collections\Sorting\NativeQuickSorter` and `\Stillat\Common\Collections\Sorting\QuickSorter`)
* Selection (`\Stillat\Common\Collections\Sorting\SelectionSorter`)
* Shell (`\Stillat\Common\Collections\Sorting\ShellSorter`)

To use any of the sorting algorithms, you can simply instantiate an instance of one of the algorithms like so:

    <?php

    Route::get('/', function()
    {
        $sorter = new Stillat\Common\Collections\Sorting\BubbleSorter;

        $sampleArray = array(
            92, 21, 'bob', 'alice'
        );

        $sortedArray = $sorter->sort($sampleArray);
        $reverseSort = $sorter->tros($sampleArray);

        // Just dump the output and exit.
        dd($sortedArray, $reverseSort);

    });

Each sorting algorithm implements the `\Stillat\Common\Collections\ArraySortingInterface`. This interface guarantees that each algorithm will have a `sort` and a `tros` function.

The `sort` function sorts a collection in an A to Z fashion, while the `tros` function sorts with a Z to A behavior (an easy way to remember this is that `tros` is `sort` spelled backwards).