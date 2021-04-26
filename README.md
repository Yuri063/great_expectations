**Проверки great_expectations для наборов данных:**
---
***

1. ***DATASET: ods_billing***
***

1.1 column='user_id' (INT)

	batch.expect_column_values_to_not_be_null(column='user_id')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='user_id', type_list=['INTEGER', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_min_to_be_between(column='user_id', max_value=None, min_value=1)
			Проверка на отсутствие неположительных значений ID в столбце
	batch.expect_column_unique_value_count_to_be_between(column='user_id', max_value=9970, min_value=1)
			Проверка количества уникальных значений в столбце

1.2 column='billing_period' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='billing_period')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='billing_period', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_values_to_match_regex(column='billing_period', regex=r'(?:19|20)[0-9]{2}-(0[1-9]|1[012])')
			Валидация по шаблону: год-месяц в виде YYYY-MM
	batch.expect_column_values_to_be_in_set(column='billing_period', value_set=['2013-01', '2013-02', ..., '2020-12'])
			Стандартная проверка на соответствие набору допустимых значений
	batch.expect_column_proportion_of_unique_values_to_be_between(column='billing_period', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)

1.3 column='service' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='service')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='service', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='service', max_value=1.0, min_value=1.0)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
			
1.4 column='tariff' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='tariff')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='tariff', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_values_to_be_in_set(column='tariff', value_set=['Gigabyte', 'Maxi', 'Megabyte', 'Mini'])
			Стандартная проверка на соответствие набору допустимых значений
	batch.expect_column_proportion_of_unique_values_to_be_between(column='tariff', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	part_tariff = great_expectations.dataset.util.categorical_partition_data(['Gigabyte', 'Maxi', 'Megabyte', 'Mini'])
	batch.expect_column_kl_divergence_to_be_less_than(column='tariff', partition_object=part_tariff, result_format='BASIC')
			Проверка коэффициента дивергенции распределний. Т.к. распределение рассматривается в данном случае в
			единственном числе, то данная проверка интересна с точки зрения визуализации гистограммы распределения
			
1.5 column='sum' (DECIMAL)

	batch.expect_column_values_to_not_be_null(column='sum')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='sum', type_list=['FLOAT', 'DOUBLE', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_min_to_be_between(column='sum',  max_value=None, min_value=0.0)
			Проверка на отсутствие отрицательных значений денежной суммы в столбце
	batch.expect_column_mean_to_be_between(column='sum', ...)
	batch.expect_column_median_to_be_between(column='sum', ...)
	batch.expect_column_quantile_values_to_be_between(column='sum', ...)
			Стандартные проверки для числовых данных в столбце (среднее, медиана, квантиль для распределения 
			выборки на равные группы). Могут использоваться для оценки корректности поступивших данных.
	batch.expect_column_proportion_of_unique_values_to_be_between(column='sum', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
			
1.6 column='created_at' (TIMESTAMP)

	batch.expect_column_values_to_not_be_null(column='created_at')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='created_at', type_list=['DATETIME', 'DATE', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='created_at', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	batch.expect_column_values_to_be_between(column='created_at', max_value=datetime.datetime.strptime('2020-12-31', '%Y-%m-%d'),
								      min_value=datetime.datetime.strptime('2012-01-01', '%Y-%m-%d'))
			Проверка всех дат в столбце на вхождение в допустимый диапазон

2. ***DATASET: ods_issue***
***

2.1 column='user_id' (INT)

	batch.expect_column_values_to_not_be_null(column='user_id')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='user_id', type_list=['INTEGER', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_min_to_be_between(column='user_id', max_value=None, min_value=1)
			Проверка на отсутствие неположительных значений ID в столбце
	batch.expect_column_unique_value_count_to_be_between(column='user_id', max_value=9970, min_value=1)
			Проверка количества уникальных значений в столбце
			
2.2 column='start_time' (TIMESTAMP)

	batch.expect_column_values_to_not_be_null(column='start_time')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='start_time', type_list=['DATETIME', 'DATE', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='start_time', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	batch.expect_column_values_to_be_between(column='start_time', max_value=datetime.datetime.strptime('2021-01-01', '%Y-%m-%d'),
								      min_value=datetime.datetime.strptime('2012-01-01', '%Y-%m-%d'))
			Проверка всех дат в столбце на вхождение в допустимый диапазон
			
2.3 column='end_time' (TIMESTAMP)

	batch.expect_column_values_to_not_be_null(column='end_time')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='end_time', type_list=['DATETIME', 'DATE', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='end_time', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	batch.expect_column_values_to_be_between(column='end_time', max_value=datetime.datetime.strptime('2021-03-31', '%Y-%m-%d'),
								      min_value=datetime.datetime.strptime('2012-01-01', '%Y-%m-%d'))
			Проверка всех дат в столбце на вхождение в допустимый диапазон
			
2.4 column='title' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='title')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='title', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='title', max_value=1.0, min_value=1.0)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
			
2.5 column='description' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='description')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='description', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='description', max_value=1.0, min_value=1.0)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
			
2.6 column='service' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='service')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='service', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_values_to_be_in_set(column='service', value_set=['Connect', 'Disconnect', 'Setup Environment'])
			Стандартная проверка на соответствие набору допустимых значений
	batch.expect_column_proportion_of_unique_values_to_be_between(column='service', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	part_issue = great_expectations.dataset.util.categorical_partition_data(['Connect', 'Disconnect', 'Setup Environment'])
	batch.expect_column_kl_divergence_to_be_less_than(column='service', partition_object=part_issue, result_format='BASIC')
			Проверка коэффициента дивергенции распределний. Т.к. распределение рассматривается в данном случае в
			единственном числе, то данная проверка интересна с точки зрения визуализации гистограммы распределения
			
			
3. ***DATASET: ods_payment***
***

3.1 column='user_id' (INT)
	batch.expect_column_values_to_not_be_null(column='user_id')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='user_id', type_list=['INTEGER', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_min_to_be_between(column='user_id', max_value=None, min_value=1)
			Проверка на отсутствие неположительных значений ID в столбце
	batch.expect_column_unique_value_count_to_be_between(column='user_id', max_value=9970, min_value=1)
			Проверка количества уникальных значений в столбце
			
3.2 column='pay_doc_type' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='pay_doc_type')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='pay_doc_type', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_values_to_be_in_set(column='service', value_set=['MASTER', 'MIR', 'VISA'])
			Стандартная проверка на соответствие набору допустимых значений
	part_doc_type = great_expectations.dataset.util.categorical_partition_data(['MASTER', 'MIR', 'VISA'])
	batch.expect_column_kl_divergence_to_be_less_than(column='pay_doc_type', partition_object=part_doc_type, result_format='BASIC')
			Проверка коэффициента дивергенции распределний. Т.к. распределение рассматривается в данном случае в
			единственном числе, то данная проверка интересна с точки зрения визуализации гистограммы распределения
			
3.3 column='pay_doc_num' (BIGINT)

	batch.expect_column_values_to_not_be_null(column='pay_doc_num')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='pay_doc_num', type_list=['INTEGER', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_min_to_be_between(column='pay_doc_num', max_value=None, min_value=1)
			Проверка на отсутствие неположительных значений ID в столбце
	batch.expect_column_unique_value_count_to_be_between(column='pay_doc_num', max_value=9970, min_value=1)
			Проверка количества уникальных значений в столбце
			
3.4 column='account' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='account')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='account', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='account', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	batch.expect_column_unique_value_count_to_be_between(column='account', max_value=9970, min_value=1)
			Проверка количества уникальных значений в столбце
			
3.5 column='phone' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='phone')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='phone', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_values_to_match_regex(column='phone', regex=r'^((8|\+7)[\- ]?)?(\(?\d{3}\)?[\- ]?)?[\d\- ]{7,10}$')
			Валидация телефона по шаблону: r'^((8|\+7)[\- ]?)?(\(?\d{3}\)?[\- ]?)?[\d\- ]{7,10}$'
	batch.expect_column_unique_value_count_to_be_between(column='phone', max_value=9970, min_value=1)
			Проверка количества уникальных значений в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='phone', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
			
3.6 column='billing_period' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='billing_period')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='billing_period', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_values_to_match_regex(column='billing_period', regex=r'(?:19|20)[0-9]{2}-(0[1-9]|1[012])')
			Валидация по шаблону: год-месяц в виде YYYY-MM
	batch.expect_column_values_to_be_in_set(column='billing_period', value_set=['2013-01', '2013-02', ..., '2020-12'])
			Стандартная проверка на соответствие набору допустимых значений
	batch.expect_column_proportion_of_unique_values_to_be_between(column='billing_period', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
			
3.7 column='pay_date' (TIMESTAMP)

	batch.expect_column_values_to_not_be_null(column='pay_date')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='pay_date', type_list=['DATETIME', 'DATE', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='pay_date', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	batch.expect_column_values_to_be_between(column='pay_date', max_value=datetime.datetime.strptime('2020-12-31', '%Y-%m-%d'),
								      min_value=datetime.datetime.strptime('2012-01-01', '%Y-%m-%d'))
								      
3.8 column='sum' (DECIMAL)

	batch.expect_column_values_to_not_be_null(column='sum')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='sum', type_list=['FLOAT', 'DOUBLE', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_min_to_be_between(column='sum',  max_value=None, min_value=0.0)
			Проверка на отсутствие отрицательных значений денежной суммы в столбце
	batch.expect_column_mean_to_be_between(column='sum', ...)
	batch.expect_column_median_to_be_between(column='sum', ...)
	batch.expect_column_quantile_values_to_be_between(column='sum', ...)
			Стандартные проверки для числовых данных в столбце (среднее, медиана, квантиль для распределения 
			выборки на равные группы). Могут использоваться для оценки корректности поступивших данных.
	batch.expect_column_proportion_of_unique_values_to_be_between(column='sum', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
			

4. ***DATASET: ods_traffic***
***

4.1 column='user_id' (INT)

	batch.expect_column_values_to_not_be_null(column='user_id')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='user_id', type_list=['INTEGER', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_min_to_be_between(column='user_id', max_value=None, min_value=1)
			Проверка на отсутствие неположительных значений ID в столбце
	batch.expect_column_unique_value_count_to_be_between(column='user_id', max_value=11041, min_value=1)
			Проверка количества уникальных значений в столбце
			
4.2 column='time_stamp' (TIMESTAMP)

	batch.expect_column_values_to_not_be_null(column='time_stamp')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='time_stamp', type_list=['DATETIME', 'DATE', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='time_stamp', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	batch.expect_column_values_to_be_between(column='time_stamp', max_value=datetime.datetime.strptime('2021-01-01', '%Y-%m-%d'),
								      min_value=datetime.datetime.strptime('2012-01-01', '%Y-%m-%d'))
								      
4.3 column='device_id' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='device_id')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='device_id', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='device_id', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	batch.expect_column_unique_value_count_to_be_between(column='account', max_value=11041, min_value=1)
			Проверка количества уникальных значений в столбце
			
4.4 column='device_ip_addr' (VARCHAR)

	batch.expect_column_values_to_not_be_null(column='device_ip_addr')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='device_ip_addr', type_list=['CHAR', 'VARCHAR', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_proportion_of_unique_values_to_be_between(column='device_ip_addr', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
	batch.expect_column_unique_value_count_to_be_between(column='device_ip_addr', max_value=11041, min_value=1)
			Проверка количества уникальных значений в столбце
	batch.expect_column_values_to_match_regex(column='device_ip_addr', regex=r'((25[0-5]|2[0-4]\d|[01]?\d\d?)\.){3}(25[0-5]|2[0-4]\d|[01]?\d\d?)')
			Валидация ip-адреса по шаблону: AAA.BBB.CCC.DDD
			
4.5 column='bytes_sent' (BIGINT)

	batch.expect_column_values_to_not_be_null(column='bytes_sent')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='bytes_sent', type_list=['INTEGER', 'integer', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_min_to_be_between(column='bytes_sent',  max_value=None, min_value=1)
			Проверка на отсутствие неположительных значений счетчика байт в столбце
	batch.expect_column_max_to_be_between(column='bytes_sent', max_value=1000000000, min_value=1)
			Проверка на отсутствие "подозрительно" больших значений счетчика байт в столбце
	batch.expect_column_mean_to_be_between(column='bytes_sent', ...)
	batch.expect_column_median_to_be_between(column='bytes_sent', ...)
	batch.expect_column_quantile_values_to_be_between(column='bytes_sent', ...)
			Стандартные проверки для числовых данных в столбце (среднее, медиана, квантиль для распределения 
			выборки на равные группы). Могут использоваться для оценки корректности поступивших данных.
	batch.expect_column_proportion_of_unique_values_to_be_between(column='bytes_sent', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
			
4.6 column='bytes_received' (BIGINT)

	batch.expect_column_values_to_not_be_null(column='bytes_received')
			Стандартная проверка на отсутствие значений NULL в столбце
	batch.expect_column_values_to_be_in_type_list(column='bytes_received', type_list=['INTEGER', 'integer', ...])
			Стандартная проверка на корректность типа данных в столбце
	batch.expect_column_min_to_be_between(column='bytes_received',  max_value=None, min_value=1)
			Проверка на отсутствие неположительных значений счетчика байт в столбце
	batch.expect_column_max_to_be_between(column='bytes_received', max_value=1000000000, min_value=1)
			Проверка на отсутствие "подозрительно" больших значений счетчика байт в столбце
	batch.expect_column_mean_to_be_between(column='bytes_received', ...)
	batch.expect_column_median_to_be_between(column='bytes_received', ...)
	batch.expect_column_quantile_values_to_be_between(column='bytes_received', ...)
			Стандартные проверки для числовых данных в столбце (среднее, медиана, квантиль для распределения 
			выборки на равные группы). Могут использоваться для оценки корректности поступивших данных.
	batch.expect_column_proportion_of_unique_values_to_be_between(column='bytes_received', ...)
			Стандартная проверка коэффициента повторяемости значений в столбце (кол-во уникальных значение/общее кол-во)
			
			 
