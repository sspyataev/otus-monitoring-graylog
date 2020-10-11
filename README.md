# otus-monitoring-graylog
При выполенении ДЗ столкнулся с тем, что требуемое не реализуемо. Судя по формулировке, в graylog должен быть input GELF UDP, соответственно filebeat должен отправлять логи по UDP. Но filebeat не поддерживает отправку по UDP (как пример - https://discuss.elastic.co/t/how-to-configure-filebeat-to-send-logs-over-udp-to-graylog/130822).
В связи с этим было сделано:
1. Установлен и настроен graylog.
2. Установлен и настроен filebeat. Конфиг во вложении.
3. Созданы два input. 1ый - GELF UDP, 2ой - Beats.
4. Создан index set
5. Созданы 2 stream. У одного input GELF UDP, у второго Beats.
6. Для stream'ов созданы правила. У stream Beats - для отображения логов содержащих информацию о sshd. У GELF UDP - по кастомному полю.
7. В stream от Beats Input логи поступают автоматически.
8. В stream GELF UDP логи создаются через отправку на input:
echo -e '{"version": "1.1","host":"example.org","short_message":"Short message 2","full_message":"Backtrace here\n\nmore stuff","level":1,"_user_id":9001,"_some_info":"foo","_some_env_var":"bar"}\0' | nc -w 1 -u localhost 40001
9. Скрины работы стримов во вложении. graylog-ssh-stream.png - из Beats Input, graylog-udp-stream.png - gelf udp.

Если ДЗ выпополнено не корректно, просьба уточнить формулировку ДЗ.
Спасибо.
