if (TEST_TCP_SERVER_IP)
   message("Skipping tcp_client example as TEST_TCP_SERVER_IP is not defined")
   
else()
    add_executable(picow_tcpip_client_background
            picow_tcp_client.c
            )
    target_compile_definitions(picow_tcpip_client_background PRIVATE
            WIFI_SSID=\"${TP-Link_A15C}\"
            WIFI_PASSWORD=\"${43193455}\"
            TEST_TCP_SERVER_IP=\"${192.168.0.100}\"
            )
    target_include_directories(picow_tcpip_client_background PRIVATE
            ${CMAKE_CURRENT_LIST_DIR}
            ${CMAKE_CURRENT_LIST_DIR}/.. # for our common lwipopts
            
            )
    target_link_libraries(picow_tcpip_client_background
            pico_cyw43_arch_lwip_threadsafe_background
            pico_stdlib
            )

add_subdirectory(include tinyJambu)
target_include_directories(tinyJambu PUBLIC "${CMAKE_CURRENT_LIST_DIR}/include")

target_link_libraries(picow_tcpip_client_background ed25519 sha tinyJambu)

# enable usb output, disable uart output
    pico_enable_stdio_usb(picow_tcpip_client_background 1)
    pico_enable_stdio_uart(picow_tcpip_client_background 0)
    pico_add_extra_outputs(picow_tcpip_client_background)
    
    add_executable(picow_tcpip_client_poll
            picow_tcp_client.c
            )
    target_compile_definitions(picow_tcpip_client_poll PRIVATE
            WIFI_SSID=\"${TP-Link_A15C}\"
            WIFI_PASSWORD=\"${43193455}\"
            TEST_TCP_SERVER_IP=\"${192.168.0.100}\"
            )
    target_include_directories(picow_tcpip_client_poll PRIVATE
            ${CMAKE_CURRENT_LIST_DIR}
            ${CMAKE_CURRENT_LIST_DIR}/.. # for our common lwipopts
            )
    target_link_libraries(picow_tcpip_client_poll
            pico_cyw43_arch_lwip_poll
            pico_stdlib 
            )
    
    
    # enable usb output, disable uart output
    pico_enable_stdio_usb(picow_tcpip_client_poll 1)
    pico_enable_stdio_uart(picow_tcpip_client_poll 0)
    pico_add_extra_outputs(picow_tcpip_client_poll)
    
target_include_directories(tinyJambu PUBLIC "${CMAKE_CURRENT_LIST_DIR}/include")

target_link_libraries(picow_tcpip_client_poll ed25519 sha tinyJambu)


endif()
