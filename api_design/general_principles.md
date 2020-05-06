# General Principles

- API Should Do One Thing and Do it well

- API Should Be As Small As Possible But No Smaller
       
       When in doubt leave it out. Because you can always add, but you can never remove. 
       Conceptual Weight
       Power to Weight Ratio
       
- Implementation Should Not Impact API
        
        Dont let the implementation details leak into the API
        Eg: Throwing an SQL Exception. This should be consumed in the implementation details
        
- Minimize Accessibility of Everything
        
        - private is better than protected is better than public
        - Making private maximizes information hiding which helps modules to be redesigned easily
        
- Names Matter : API is a little language

        Be consistent. Eg: Remove/Delete
        
- Documentation Matters

        Document Religiously that is public
            class : a simple noun phrase
            methods : precondition, postcondition and side effects
            parameters : mention units if any
        
- Performance Consequences of API Design Decisions

- API Must Coexist Peacefully with Platform
        
        Don't Transliterate the API
        Taking advantage of underlying constructs
     
