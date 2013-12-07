#PHP SQL Parser
This project is a pure PHP SQL parser.  

Many thanks to Andre who contributes to and maintains the parser!

----

##Download ##
  * http://code.google.com/p/php-sql-parser/downloads/list
  * http://php-sql-parser.googlecode.com/svn/trunk/example.php

###Full support for the MySQL dialect for the following statement types###
  * SELECT
  * INSERT
  * UPDATE
  * DELETE
  * REPLACE
  * SET
  * DROP

###Other SQL statement types###
Other statements are returned as an array of tokens.  This is not as structured as the information available about the above types.  See the ParserManual for more information.

###Other SQL dialects###
Since the MySQL SQL dialect is very close to SQL-92, this should work for most database applications that need a SQL parser.  If using another database dialect, then you may want to change the reserved words - see the ParserManual.  It supports UNION, subqueries and compound statements.  

###External dependencies###
The parser is a self contained class.  It has no external dependencies.  The parser uses a small amount of regex.

###Focus###
The focus of the parser is complete and accurate support for the MySQL SQL dialect.  The focus is not on optimizing for performance.  It is expected that you will present syntactically valid queries.  

###Manual###
ParserManual - Check out the manual here

*Example Output (via print_r)*
----

 
    $parser = new PHPSQLParser();

    $sql = "SELECT q.qid, question, gid 
              FROM questions as q 
             WHERE (select count(*) 
                      from answers as a 
                     where a.qid=q.qid and scale_id=0)=0 
               and sid=11929 AND type IN ('F', 'H', 'W', 'Z', '1') 
               and q.parent_qid=0";
 
    $p = $parser->parse($sql);
 
    print_r($p);

    Array
    (
    [SELECT] => Array
        (
            [0] => Array
                (
                    [expr_type] => colref
                    [alias] =>
                    [base_expr] => q.qid
                    [no_quotes] => q.qid
                    [sub_tree] =>
                )

            [1] => Array
                (
                    [expr_type] => colref
                    [alias] =>
                    [base_expr] => question
                    [no_quotes] => question
                    [sub_tree] =>
                )

            [2] => Array
                (
                    [expr_type] => colref
                    [alias] =>
                    [base_expr] => gid
                    [no_quotes] => gid
                    [sub_tree] =>
                )

        )

    [FROM] => Array
        (
            [0] => Array
                (
                    [expr_type] => table
                    [table] => questions
                    [no_quotes] => questions
                    [alias] => Array
                        (
                            [as] => 1
                            [name] => q
                            [base_expr] => as q
                            [no_quotes] => q
                        )

                    [join_type] => JOIN
                    [ref_type] =>
                    [ref_clause] =>
                    [base_expr] => questions as q
                    [sub_tree] =>
                )

        )

    [WHERE] => Array
        (
            [0] => Array
                (
                    [expr_type] => subquery
                    [base_expr] => (select count(*) from answers as a where a.qid=q.qid and scale_id=0)
                    [sub_tree] => Array
                        (
                            [SELECT] => Array
                                (
                                    [0] => Array
                                        (
                                            [expr_type] => aggregate_function
                                            [alias] =>
                                            [base_expr] => count
                                            [sub_tree] => Array
                                                (
                                                    [0] => Array
                                                        (
                                                            [expr_type] => colref
                                                            [base_expr] => *
                                                            [sub_tree] =>
                                                        )

                                                )

                                        )

                                )

                            [FROM] => Array
                                (
                                    [0] => Array
                                        (
                                            [expr_type] => table
                                            [table] => answers
                                            [no_quotes] => answers
                                            [alias] => Array
                                                (
                                                    [as] => 1
                                                    [name] => a
                                                    [base_expr] => as a
                                                    [no_quotes] => a
                                                )

                                            [join_type] => JOIN
                                            [ref_type] =>
                                            [ref_clause] =>
                                            [base_expr] => answers as a
                                            [sub_tree] =>
                                        )

                                )

                            [WHERE] => Array
                                (
                                    [0] => Array
                                        (
                                            [expr_type] => colref
                                            [base_expr] => a.qid
                                            [no_quotes] => a.qid
                                            [sub_tree] =>
                                        )

                                    [1] => Array
                                        (
                                            [expr_type] => operator
                                            [base_expr] => =
                                            [sub_tree] =>
                                        )

                                    [2] => Array
                                        (
                                            [expr_type] => colref
                                            [base_expr] => q.qid
                                            [no_quotes] => q.qid
                                            [sub_tree] =>
                                        )

                                    [3] => Array
                                        (
                                            [expr_type] => operator
                                            [base_expr] => and
                                            [sub_tree] =>
                                        )

                                    [4] => Array
                                        (
                                            [expr_type] => colref
                                            [base_expr] => scale_id
                                            [no_quotes] => scale_id
                                            [sub_tree] =>
                                        )

                                    [5] => Array
                                        (
                                            [expr_type] => operator
                                            [base_expr] => =
                                            [sub_tree] =>
                                        )

                                    [6] => Array
                                        (
                                            [expr_type] => const
                                            [base_expr] => 0
                                            [sub_tree] =>
                                        )

                                )

                        )

                )

            [1] => Array
                (
                    [expr_type] => operator
                    [base_expr] => =
                    [sub_tree] =>
                )

            [2] => Array
                (
                    [expr_type] => const
                    [base_expr] => 0
                    [sub_tree] =>
                )

            [3] => Array
                (
                    [expr_type] => operator
                    [base_expr] => and
                    [sub_tree] =>
                )

            [4] => Array
                (
                    [expr_type] => colref
                    [base_expr] => sid
                    [no_quotes] => sid
                    [sub_tree] =>
                )

            [5] => Array
                (
                    [expr_type] => operator
                    [base_expr] => =
                    [sub_tree] =>
                )

            [6] => Array
                (
                    [expr_type] => const
                    [base_expr] => 11929
                    [sub_tree] =>
                )

            [7] => Array
                (
                    [expr_type] => operator
                    [base_expr] => AND
                    [sub_tree] =>
                )

            [8] => Array
                (
                    [expr_type] => colref
                    [base_expr] => type
                    [no_quotes] => type
                    [sub_tree] =>
                )

            [9] => Array
                (
                    [expr_type] => operator
                    [base_expr] => IN
                    [sub_tree] =>
                )

            [10] => Array
                (
                    [expr_type] => in-list
                    [base_expr] => ('F', 'H', 'W', 'Z', '1')
                    [sub_tree] => Array
                        (
                            [0] => Array
                                (
                                    [expr_type] => const
                                    [base_expr] => 'F'
                                    [sub_tree] =>
                                )

                            [1] => Array
                                (
                                    [expr_type] => const
                                    [base_expr] => 'H'
                                    [sub_tree] =>
                                )

                            [2] => Array
                                (
                                    [expr_type] => const
                                    [base_expr] => 'W'
                                    [sub_tree] =>
                                )

                            [3] => Array
                                (
                                    [expr_type] => const
                                    [base_expr] => 'Z'
                                    [sub_tree] =>
                                )

                            [4] => Array
                                (
                                    [expr_type] => const
                                    [base_expr] => '1'
                                    [sub_tree] =>
                                )

                        )

                )

            [11] => Array
                (
                    [expr_type] => operator
                    [base_expr] => and
                    [sub_tree] =>
                )

            [12] => Array
                (
                    [expr_type] => colref
                    [base_expr] => q.parent_qid
                    [no_quotes] => q.parent_qid
                    [sub_tree] =>
                )

            [13] => Array
                (
                    [expr_type] => operator
                    [base_expr] => =
                    [sub_tree] =>
                )

            [14] => Array
                (
                    [expr_type] => const
                    [base_expr] => 0
                    [sub_tree] =>
                )

        )

    )
