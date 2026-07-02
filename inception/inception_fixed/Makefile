all:
	mkdir -p /home/asmafrid/data/mariadb
	mkdir -p /home/asmafrid/data/wordpress
	docker-compose -f srcs/docker-compose.yml up -d --build

down:
	docker-compose -f srcs/docker-compose.yml down

clean:
	docker-compose -f srcs/docker-compose.yml down -v
	docker system prune -f

fclean: clean
	rm -rf /home/asmafrid/data/mariadb
	rm -rf /home/asmafrid/data/wordpress

re: fclean all

.PHONY: all down clean fclean re
