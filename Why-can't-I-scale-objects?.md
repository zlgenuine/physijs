Scaling is the one aspect of Three's mesh that was purposefully left out -

* It is not supported by most (any?) physics libraries, therefore:
* Scaling an object after creation would require a new physics body be created (which is is not cost-free)
* I would rather this cost be apparent to the developer by forcing a whole new object be created

If you have a good use case for including scaling please [open an issue](https://github.com/chandlerprall/Physijs/issues/new) and let me know.