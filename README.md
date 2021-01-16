 NetRuleEngine
 ==============
C# simple Rule Engine. High performance object rule matching. Support various complex grouped predeicates.
available on [nuget](https://www.nuget.org/packages/NetRuleEngine/).

(Input) An Object + Rule(s) => (Output) Is Match

[![Build Status](https://travis-ci.com/AmirSasson/NetRuleEngine.svg?branch=main)](https://travis-ci.com/AmirSasson/NetRuleEngine)

#### Use cases
- Bussiness rules that are dynamicaly generated by a user interface, to dermine Yes/No conditions
- Audience Matching
- Dynamic Alerts detection


#### Simple usage:

```
    var engine = new RulesService<TestModel>(new RulesCompiler(), new LazyCache.Mocks.MockCachingService());
            
    var matching = engine.GetMatchingRules(
        new TestModel { NumericField = 5 },
        new[] {
            new RulesConfig {
                Id = Guid.NewGuid(),
                RulesOperator = Rule.InterRuleOperatorType.And,
                RulesGroups = new RulesGroup[] {
                    new RulesGroup {
                        RulesOperator = Rule.InterRuleOperatorType.And,
                        Rules = new[] {
                            new Rule { 
                            ComparisonOperator = Rule.ComparisonOperatorType.Equal,
                            ComparisonValue = 5.ToString(),
                            ComparisonPredicate = nameof(TestModel.NumericField) 
                            }
                        }
                    }
                }
            }
        });
```

- depenent on LazyCache to store compiles rules.
- compiles Expression Trees into dynamic cached code to support high performance usage.

Features:
- composite objects
- enums
- string
- numbers
- datetime
- Dictionaries
- collections

and many more. See units test for full usage scenarios.