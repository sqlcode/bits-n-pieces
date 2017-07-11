
JavaScript Expression Evaluator to Aggregation
==============================================

Based almost entirely on [JavaScript Expression Evaluator](https://github.com/silentmatt/expr-eval)

Description
-------------------------------------

Parses and evaluates mathematical expressions. Provides method to convert them to aggregation expression.

See [original project README](https://github.com/silentmatt/expr-eval/blob/master/README.md) for details.

Installation
-------------------------------------

In mongo shell:

    > load('parser.js')

Or 
    mongo parser.js --shell

Basic Usage
-------------------------------------

    > var parser = new Parser();
    > var expr = parser.parse('2 * x + 1');
    > agg1=expr.toAgg()
    > agg1
    { "$add" : [ { "$multiply" : [ 2, "x" ] }, 1 ] }
    > expressionToString(aggToTokens(a1),false)
    ((2 * "x") + 1)

    > formula="100*(50 - min(10, (length('$str1')-length('$str2'))))";
    > var expr = parser.parse(fomula);
    > expr.toAgg()
    {
        "$multiply" : [
            100,
            {
                "$subtract" : [
                    50,
                    {
                        "$min" : [
                            10,
                            {
                                "$subtract" : [
                                    {
                                        "$strLenCP" : [
                                            "$str1"
                                        ]
                                    },
                                    {
                                        "$strLenCP" : [
                                            "$str2"
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        ]
    }
    // and back
    > expressionToString(aggToTokens(e.toAgg()),false)
    (100 * (50 - min(10, ((length "$str1") - (length "$str2")))))
