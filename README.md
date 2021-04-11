# Limit-Order-Book-Trading-in-python
 it would maintain both buy side and sell side of Order. You need to Implement Market Order, Limit Order and Stop Order.
states = []
current_timestamp = None
current_state = {}

for timestamp, (id_, price, exch, size) in df.iterrows():
    if current_timestamp is None:
        current_timestamp = timestamp
    if current_timestamp != timestamp:
        for key in list(current_state):
            if current_state[key] == 0.:
                del current_state[key]
        states.append((current_timestamp, dict(**current_state)))
        current_timestamp = timestamp
    key = (exch, price)
    current_state.setdefault(key, 0.)
    current_state[key] += size
states.append((timestamp, dict(**current_state)))

order_book = pd.DataFrame.from_items(states).T
