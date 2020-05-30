# Design Classes

- Minimize mutability
        
        By default classes should be made immutable unless there is a good reason to do otherwise
        If mutable, keep the state-space small and well-defined
        
- Subclass only when it makes sense
        
        Guiding Principle: 
            If its is-a relationship then subclass else composition.
            Public classes should not subclass other public classes
            
- Design and Document for Inheritance or Else Prohibit it
        
        Conservative policy: all concrete classes must be final 
         