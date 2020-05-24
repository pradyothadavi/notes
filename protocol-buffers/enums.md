# Enums in proto

enums/feature_category.proto:10:3: Note that enum values use C++ scoping rules, meaning that enum values are siblings of their type, not children of it.  Therefore, "NOT_DEFINED" must be unique within "enums", not just within "FeatureCategory".

```proto
syntax = "proto3";

package enums;

enum First {

  NOT_DEFINED = 0;

  F1 = 1;

  F2 = 2;
}
```

```proto
syntax = "proto3";

package enums;

enum Second {

  NOT_DEFINED = 0;

  S1 = 1;

  S2 = 2;
}
```