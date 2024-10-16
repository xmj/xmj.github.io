DevOps Done Wrong
=================

The following articles detail the many ways I have seen that my clients past and present succeeded in doing injustice to a very useful collaboration model.

* [Big Data Frameworks](01_big_data_frameworks.md)
  On using frameworks that "facilitate big data management", and incentives.
* [Environment Multiplication](02_environment_multiplication.md)
  On using audience-driven environments and makework.
* [Missing Code Reviews](03_missing_reviews.md)
  On creating common knowledge through code reviews.
* [Continuing Silos](04_silos.md)
  On how DevOps continues corporate siloing.
* [Hybrid Games](05_hybrid_games.md)
  On Hybrid Clouds, processes, and bringing the wrong mindset.
* [Agile Waterfalls](06_agile_waterfalls.md)
  On Agile Waterfalls and the Worst of both Worlds
* [Fragile Processes](07_fragile_processes.md)
  On Fragile Processes, both bottom-up and top-down, and how to find the middle ground.
* [Systems Ownership](08_systems_ownership.md)
  On the mismatch between responsibility for, and ultimately the ability to control something.

The articles have been compiled into an ebook and can be found as [EPUB](https://xmj.me/library/DDW.epub) and [PDF](https://xmj.me/library/DDW.pdf) 

## To generate a PDF

```
pandoc 0*.md --toc --metadata-file=metadata.yml --template template/pdf.tex -o test.pdf
```

## to generate an EPUB container

```
pandoc 0*.md --css=template/style.css --toc --metadata-file=metadata.yml --template template/epub.html -o test.epub
```
