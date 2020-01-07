# Exceptions and backtrace

```
try{
    throw std::exceptions::IndexOverflowException("too big");
}
catch(const std::exceptions::IndexOverflowException e){
    std::file::stdOut->print(e.msg());
}
catch(const std::exceptions::IndexUnderflowException e){
    std::file::stdOut->print(e.msg());
}
```
