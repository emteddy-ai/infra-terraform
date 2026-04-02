#!/usr/bin/env python3

import os
import sys
import json
import yaml
import logging

from . import config
from . import utils

def read_file(filename):
    with open(filename, 'r') as f:
        return f.read()

def write_file(filename, content):
    with open(filename, 'w') as f:
        f.write(content)

def load_config():
    return config.load()

def save_config(config):
    config.save()

def load_yaml_config():
    return yaml.safe_load(read_file('config.yaml'))

def save_yaml_config(config):
    with open('config.yaml', 'w') as f:
        yaml.dump(config, f, default_flow_style=False)

def load_json_config():
    return json.load(read_file('config.json'))

def save_json_config(config):
    with open('config.json', 'w') as f:
        json.dump(config, f, indent=4)

def main():
    config = load_config()
    config.load_yaml_config()
    config.save_yaml_config()

    if os.path.exists('config.json'):
        config.load_json_config()
        config.save_json_config()

if __name__ == '__main__':
    main()