# Named Parameter for Pascal

```pascal
// PASCAL NAMED PARAMETER PROPOSAL
// AS {$MODESWITCH NAMEDPARAMETER}

// function declaration with some default values
function f(i: integer = 0; s: string = ''; d: double): boolean;
begin
  result := true;
end;

// Old fashioned function calling,
// all params must be in order but
// allowed to skip default params.
f(0.1);
f('abc',0.1);
f(3,'abc',0.1);

// Mixed style function calling,
// still respects the params order
// if NOT all params name is given.
f(s := 'def', 0.2);
f(4, s := 'def', 0.2);

// New style function calling,
// params don't need to be in order
// if ALL params name is given.
f(d := 0.3, i := 5);      // s = default
f(s := 'ghi', d := 0.3);  // i = default
f(i := 5, d := 0.3, s := 'ghi');

// Fills param using other variable,
// compiler knows which is what.
s := 'text';
d := 0.4;
f(s := s, d);
f(d := d, s := s);

// It should also work on `procedure` as well.
```
———  
I welcome your comment [here](https://github.com/pakLebah/paklebah.github.io/issues/2).  
Thank you. 😊

---
← [back to Home](index.md)
