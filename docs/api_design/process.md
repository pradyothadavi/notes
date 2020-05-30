# Process of API Design

## Characteristics of a Good API
- Easy to learn
- Easy to use, even without documentation
- Hard to misuse
- Easy to read and maintain code that uses it
- **Sufficiently** powerful to satisfy requirements
- Easy to extend
- Appropriate to audience

### Gather Requirements
- Your responsibility to get the true requirements
- Understand the use-cases. 
- Prepare a list of tasks that the API needs to be preform in order to be successful.
- More rewarding to build something generic, however be mindful not to over engineer. 

### Write a One Page Spec

### Write to your API
- These will later form your validate test cases

### Service Provider Interface ( SPI )
- Test the interface for atleast 3 sources ( Will Tracz - Rules of Threes )

        Eg: An SPI for an object model to persist must be tested against InMemory, SQL and Document Store
        
### Maintain Realistic Expectations
- Displease everyone at the same level as against pleasing some one specifically. 