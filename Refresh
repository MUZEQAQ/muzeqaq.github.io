import requests
import schedule
import random
import logging
import time
from colorama import init, Fore

init(autoreset=True)


def logger(file_log):
    '''
    打日志
    :param file_log: 日志文件名，类型string；
    '''
    # 创建一个loggger，并设置日志级别
    logger = logging.getLogger()
    logger.setLevel(logging.DEBUG)

    # 创建一个handler，用于写入日志文件，并设置日志级别，mode:a是追加写模式，w是覆盖写模式
    fh = logging.FileHandler(filename=file_log, encoding='utf-8', mode='w')
    fh.setLevel(logging.INFO)

    # 创建一个handler，用于将日志输出到控制台，并设置日志级别
    ch = logging.StreamHandler()
    ch.setLevel(logging.INFO)

    # 定义handler的输出格式
    formatter = logging.Formatter(
        '%(asctime)s-%(name)s-%(filename)s-[line:%(lineno)d]''-%(levelname)s-[日志信息]: %(message)s')
    fh.setFormatter(formatter)
    ch.setFormatter(formatter)
    # 给logger添加handler
    logger.addHandler(fh)
    logger.addHandler(ch)


def getData():
    try:
        user_agent_pool = [  # User-Agent池
            # Cent Browser 4.3.9.248，Chromium 86.0.4240.198，2021.01
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36',

            # Edge
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36 Edg/93.0.961.38',
            # 2021.09
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36 Edg/93.0.961.44',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36 Edg/93.0.961.47',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36 Edg/93.0.961.52',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.61 Safari/537.36 Edg/94.0.992.31',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.61 Safari/537.36 Edg/94.0.992.37',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.71 Safari/537.36 Edg/94.0.992.38',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36 Edg/94.0.992.47',
            # 2021.10
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36 Edg/94.0.992.50',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36 Edg/95.0.1020.30',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36 Edg/95.0.1020.40',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.69 Safari/537.36 Edg/95.0.1020.44',
            # 2021.11
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.69 Safari/537.36 Edg/95.0.1020.53',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36 Edg/96.0.1054.29',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.55 Safari/537.36 Edg/96.0.1054.34',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.55 Safari/537.36 Edg/96.0.1054.41',
            # 2021.12
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.55 Safari/537.36 Edg/96.0.1054.43',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.93 Safari/537.36 Edg/96.0.1054.53',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.62',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36 Edg/97.0.1072.55',
            # 2022.01
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36 Edg/97.0.1072.62',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.99 Safari/537.36 Edg/97.0.1072.69',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.99 Safari/537.36 Edg/97.0.1072.76',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36 Edg/98.0.1108.43',
            # 2022.02
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36 Edg/98.0.1108.50',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36 Edg/98.0.1108.55',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36 Edg/98.0.1108.56',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36 Edg/98.0.1108.62',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.51 Safari/537.36 Edg/99.0.1150.30',
            # 2022.03
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.51 Safari/537.36 Edg/99.0.1150.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.51 Safari/537.36 Edg/99.0.1150.39',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36 Edg/99.0.1150.46',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36 Edg/99.0.1150.52',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36 Edg/99.0.1150.55',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.60 Safari/537.36 Edg/100.0.1185.29',
            # 2022.04
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.75 Safari/537.36 Edg/100.0.1185.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.75 Safari/537.36 Edg/100.0.1185.39',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36 Edg/100.0.1185.44',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36 Edg/100.0.1185.50',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Safari/537.36 Edg/101.0.1210.32',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36 Edg/101.0.1210.39',
            # 2022.05
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.64 Safari/537.36 Edg/101.0.1210.47',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.64 Safari/537.36 Edg/101.0.1210.53',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.5005.63 Safari/537.36 Edg/102.0.1245.30',
            # 2022.06
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.5005.63 Safari/537.36 Edg/102.0.1245.33',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.5005.63 Safari/537.36 Edg/102.0.1245.39',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.5005.124 Safari/537.36 Edg/102.0.1245.41',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.5005.124 Safari/537.36 Edg/102.0.1245.44',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.53 Safari/537.36 Edg/103.0.1264.37',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.66 Safari/537.36 Edg/103.0.1264.44',
            # 2022.07
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.114 Safari/537.36 Edg/103.0.1264.49',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.114 Safari/537.36 Edg/103.0.1264.62',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.134 Safari/537.36 Edg/103.0.1264.71',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.134 Safari/537.36 Edg/103.0.1264.77',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.81 Safari/537.36 Edg/104.0.1293.47',
            # 2022.08
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.81 Safari/537.36 Edg/104.0.1293.54',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.102 Safari/537.36 Edg/104.0.1293.63',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.102 Safari/537.36 Edg/104.0.1293.70',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36 Edg/105.0.1343.27',
            # 2022.09
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36 Edg/105.0.1343.33',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36 Edg/105.0.1343.42',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36 Edg/105.0.1343.50',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36 Edg/105.0.1343.53',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.34',
            # 2022.10
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.37',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.42',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.47',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.52',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36 Edg/107.0.1418.24',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36 Edg/107.0.1418.26',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36 Edg/107.0.1418.35',
            # 2022.11
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36 Edg/107.0.1418.42',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36 Edg/107.0.1418.52',

            # Chrome
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.61 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.71 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36',
            # 2021.10
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.69 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36',
            # 2021.11
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.93 Safari/537.36',
            # 2021.12
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36',
            # 2022.01
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.99 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.81 Safari/537.36',
            # 2022.02
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.82 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.51 Safari/537.36',
            # 2022.03
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.82 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.60 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.75 Safari/537.36',
            # 2022.04
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.88 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36',
            # 2022.05
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.64 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.67 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.5005.63 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.5005.115 Safari/537.36',
            # 2022.06
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.53 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.66 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.114 Safari/537.36',
            # 2022.07
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.134 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.81 Safari/537.36',
            # 2022.08
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.102 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.5195.54 Safari/537.36',
            # 2022.09
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.5195.102 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.5195.127 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.5249.91 Safari/537.36',
            # 2022.10
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.5249.103 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.5249.119 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.5304.63 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.5304.88 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.5304.106 Safari/537.36',
            # 2022.11
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.5304.107 Safari/537.36',

            # Chrome Beta
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.41 Safari/537.36',
            # 2021.09
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.17 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.32 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.40 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.49 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.18 Safari/537.36',
            # 2021.10
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.27 Safari/537.36',
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.35 Safari/537.36',
            # 2021.11
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36',

            # Firefox
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:92.0) Gecko/20100101 Firefox/92.0',  # 2021.09
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:93.0) Gecko/20100101 Firefox/93.0',  # 2021.10
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:94.0) Gecko/20100101 Firefox/94.0',  # 2021.11
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:95.0) Gecko/20100101 Firefox/95.0',  # 2021.12
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:96.0) Gecko/20100101 Firefox/96.0',  # 2022.01
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:97.0) Gecko/20100101 Firefox/97.0',  # 2022.02
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:98.0) Gecko/20100101 Firefox/98.0',  # 2022.03
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:99.0) Gecko/20100101 Firefox/99.0',  # 2022.04
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:100.0) Gecko/20100101 Firefox/100.0',  # 2022.05
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:101.0) Gecko/20100101 Firefox/101.0',  # 2022.06
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:102.0) Gecko/20100101 Firefox/102.0',  # 2022.06
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:103.0) Gecko/20100101 Firefox/103.0',  # 2022.07
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:104.0) Gecko/20100101 Firefox/104.0',  # 2022.08
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:105.0) Gecko/20100101 Firefox/105.0',  # 2022.09
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:106.0) Gecko/20100101 Firefox/106.0',  # 2022.10
            'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:107.0) Gecko/20100101 Firefox/107.0',  # 2022.11
        ]

        headers = {}
        headers['User-Agent'] = random.choice(user_agent_pool)

        url1 = 'https://api.bilibili.com/x/space/acc/info?mid=686127&jsonp=jsonp'
        url2 = 'https://api.bilibili.com/x/space/acc/info?mid=1993302&jsonp=jsonp'
        url3 = 'https://api.bilibili.com/x/space/acc/info?mid=1867191&jsonp=jsonp'
        url4 = 'https://api.bilibili.com/x/space/acc/info?mid=630077416&jsonp=jsonp'
        url5 = 'https://api.bilibili.com/x/space/acc/info?mid=22454199&jsonp=jsonp'
        url6 = 'https://api.bilibili.com/x/space/acc/info?mid=66359608&jsonp=jsonp'
        url7 = 'https://api.bilibili.com/x/space/acc/info?mid=583347&jsonp=jsonp'
        url8 = 'https://api.bilibili.com/x/space/acc/info?mid=5758670&jsonp=jsonp'
        url9 = 'https://api.bilibili.com/x/space/acc/info?mid=9208606&jsonp=jsonp'
        url10 = 'https://api.bilibili.com/x/space/acc/info?mid=347387527&jsonp=jsonp'

        res1 = requests.get(url=url1, headers=headers).json()
        res2 = requests.get(url=url2, headers=headers).json()
        res3 = requests.get(url=url3, headers=headers).json()
        res4 = requests.get(url=url4, headers=headers).json()
        res5 = requests.get(url=url5, headers=headers).json()
        res6 = requests.get(url=url6, headers=headers).json()
        res7 = requests.get(url=url7, headers=headers).json()
        res8 = requests.get(url=url8, headers=headers).json()
        res9 = requests.get(url=url9, headers=headers).json()
        res10 = requests.get(url=url10, headers=headers).json()

        a1 = "未开播" if res1['data']['live_room']['liveStatus'] == 0 else "开播"
        a2 = "未开播" if res2['data']['live_room']['liveStatus'] == 0 else "开播"
        a3 = "未开播" if res3['data']['live_room']['liveStatus'] == 0 else "开播"
        a4 = "未开播" if res4['data']['live_room']['liveStatus'] == 0 else "开播"
        a5 = "未开播" if res5['data']['live_room']['liveStatus'] == 0 else "开播"
        a6 = "未开播" if res6['data']['live_room']['liveStatus'] == 0 else "开播"
        a7 = "未开播" if res7['data']['live_room']['liveStatus'] == 0 else "开播"
        a8 = "未开播" if res8['data']['live_room']['liveStatus'] == 0 else "开播"
        a9 = "未开播" if res9['data']['live_room']['liveStatus'] == 0 else "开播"
        a10 = "未开播" if res10['data']['live_room']['liveStatus'] == 0 else "开播"

        b1 = "【" + res1['data']['live_room']['title'] + "】"
        b2 = "【" + res2['data']['live_room']['title'] + "】"
        b3 = "【" + res3['data']['live_room']['title'] + "】"
        b4 = "【" + res4['data']['live_room']['title'] + "】"
        b5 = "【" + res5['data']['live_room']['title'] + "】"
        b6 = "【" + res6['data']['live_room']['title'] + "】"
        b7 = "【" + res7['data']['live_room']['title'] + "】"
        b8 = "【" + res8['data']['live_room']['title'] + "】"
        b9 = "【" + res9['data']['live_room']['title'] + "】"
        b10 = "【" + res10['data']['live_room']['title'] + "】"

        c1 = "#9966FFCC" if a1 == "开播" else "#00000000"
        c2 = "#9966FFCC" if a2 == "开播" else "#00000000"
        c3 = "#9966FFCC" if a3 == "开播" else "#00000000"
        c4 = "#9966FFCC" if a4 == "开播" else "#00000000"
        c5 = "#9966FFCC" if a5 == "开播" else "#00000000"
        c6 = "#9966FFCC" if a6 == "开播" else "#00000000"
        c7 = "#9966FFCC" if a7 == "开播" else "#00000000"
        c8 = "#9966FFCC" if a8 == "开播" else "#00000000"
        c9 = "#9966FFCC" if a9 == "开播" else "#00000000"
        c10 = "#9966FFCC" if a10 == "开播" else "#00000000"

        f1 = open("index.html", "w+", encoding="utf-8")

        a = """
        <local:MyCard Title="" Width="28" HorizontalAlignment="Right" Margin="0,-20,0,0">
            <local:MyButton Margin="0,0,0,0" Width="30" Height="20" Background="{DynamicResource ColorBrush5}" HorizontalAlignment="Right" Padding="0,0,0,0" Text="刷新" EventType="刷新主页" ToolTip="刷新信息"/>
        </local:MyCard>
        <local:MyCard Title="籽岷团队 - 直播间" CanSwap="True"   IsSwaped="false">
            <StackPanel Margin="25,40,23,15">
                <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/zi__min" Title=\"""" + res1['data'][
            'name'] + "\t" + b1 + """\" Info=\"""" + a1 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/544853" 
                                  Background=\"""" + c1 + """\"
                                  Type="Clickable" />
                    <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/miku_master" Title=\"""" + res2['data'][
                'name'] + "\t" + b2 + """\" Info=\"""" + a2 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/1575100" 
                                  Background=\"""" + c2 + """\"
                                  Type="Clickable" />
                    <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/kai_qi" Title=\"""" + res3['data'][
                'name'] + "\t" + b3 + """\" Info=\"""" + a3 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/726800" 
                                  Background=\"""" + c3 + """\"
                                  Type="Clickable" />
                    <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/hanaowo" Title=\"""" + res4['data'][
                'name'] + "\t" + b4 + """\" Info=\"""" + a4 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/22625568" 
                                  Background=\"""" + c4 + """\"
                                  Type="Clickable" />
                    <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/juanjuanzi" Title=\"""" + res5['data'][
                'name'] + "\t" + b5 + """\" Info=\"""" + a5 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/22769463" 
                                  Background=\"""" + c5 + """\"
                                  Type="Clickable" />
                    <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/ziyinmy" Title=\"""" + res6['data'][
                'name'] + "\t" + b6 + """\" Info=\"""" + a6 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/2572741" 
                                  Background=\"""" + c6 + """\"
                                  Type="Clickable" />
                    <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/Unclechong" Title=\"""" + res7['data'][
                'name'] + "\t" + b7 + """\" Info=\"""" + a7 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/718905" 
                                  Background=\"""" + c7 + """\"
                                  Type="Clickable" />
                    <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/ginraku_o3o" Title=\"""" + res8['data'][
                'name'] + "\t" + b8 + """\" Info=\"""" + a8 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/228729" 
                                  Background=\"""" + c8 + """\"
                                  Type="Clickable" />
                    <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/ni_ca" Title=\"""" + res9['data'][
                'name'] + "\t" + b9 + """\" Info=\"""" + a9 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/4835374" 
                                  Background=\"""" + c9 + """\"
                                  Type="Clickable" />
            </StackPanel>
        </local:MyCard>
        <local:MyCard Title="之夏 - 直播间" CanSwap="True"   IsSwaped="True">
            <StackPanel Margin="25,40,23,15">
                <local:MyListItem 
                                  Logo="https://mineskin.eu/helm/zhixia_" Title=\"""" + res10['data'][
                'name'] + "\t" + b10 + """\" Info=\"""" + a10 + """\"
                                  EventType="打开网页" 
                                  EventData="https://live.bilibili.com/12529538" 
                                  Background=\"""" + c10 + """\"
                                  Type="Clickable"
                                  />
            </StackPanel>
        </local:MyCard>   
        """
        f1.write(a)
        print(
            Fore.GREEN + "读写成功 " + " " + Fore.YELLOW + time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time())))
        print(res1['data']['name'] + " " + Fore.GREEN + a1)
        print(res2['data']['name'] + " " + Fore.GREEN + a2)
        print(res3['data']['name'] + " " + Fore.GREEN + a3)
        print(res4['data']['name'] + " " + Fore.GREEN + a4)
        print(res5['data']['name'] + " " + Fore.GREEN + a5)
        print(res6['data']['name'] + " " + Fore.GREEN + a6)
        print(res7['data']['name'] + " " + Fore.GREEN + a7)
        print(res8['data']['name'] + " " + Fore.GREEN + a8)
        print(res9['data']['name'] + " " + Fore.GREEN + a9)
        print(res10['data']['name'] + " " + Fore.GREEN + a10)
        print()
        print()
        logger('./test.log')

    except:
        c = "读写失败"
        print(f"\033[0;31m{c}\033[0m")
        logger('./test.log')


if __name__ == '__main__':
    getData()
