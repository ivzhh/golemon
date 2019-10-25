add_custom_target(simple_ast_gen_y ALL
    ${CMAKE_BINARY_DIR}/lemon-parser -T${CMAKE_SOURCE_DIR}/lempar.go ${CMAKE_CURRENT_SOURCE_DIR}/parser.y
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/parser.y
    BYPRODUCTS ${CMAKE_CURRENT_SOURCE_DIR}/parser.go ${CMAKE_CURRENT_SOURCE_DIR}/parser.out ${CMAKE_CURRENT_SOURCE_DIR}/parser_tokens.go
)

add_custom_target(simple_ast ALL
    go build
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/ast.go
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)

add_custom_target(simple_ast_run ALL
    ${CMAKE_CURRENT_SOURCE_DIR}/simple_ast
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)

add_dependencies(simple_ast_gen_y lemon-parser)
add_dependencies(simple_ast simple_ast_gen_y)
add_dependencies(simple_ast_run simple_ast)