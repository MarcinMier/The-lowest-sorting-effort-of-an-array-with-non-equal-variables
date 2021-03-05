import sys


def find(val_pos, tab1, tab2):  # finding position of variables in the singe cycle
    if s_array == []:           # val_pos = position of the variable
        s_array.append(tab1[val_pos])
    if tab1[val_pos] == tab2[val_pos]:
        return None
    if tab1[val_pos] != tab2[val_pos]:
        for position, value in enumerate(tab1):
            if value == tab2[val_pos]:
                s_array.append(value)
                em_order[position] = em_order[val_pos]
                em_order[val_pos] = value
                break
        find(position, tab1, tab2)


def the_lightest(tab1):  # mass of the lightest element
    result = 7000        # maximum weight is 6500
    for li in tab1:
        if li < result:
            result = li
    return result


def mass_s_cycle(single_cycle):  # total mass of the single cycle
    sum1 = 0
    for e in single_cycle:
        for f in range(len(em_order_copy)):
            if e == em_order_copy[f]:
                sum1 += m_elements[f]
                break
    return sum1


def mass_light_cycle(tab1):  # mass of the lightest in cycle
    result = 7000            # maximum weight is 6500
    for w in tab1:
        for z in range(len(em_order_copy)):
            if w == em_order_copy[z]:
                if result > m_elements[z]:
                    result = m_elements[z]
    return result


if __name__ == '__main__':

    input_matrix = [line.rstrip('\n') for line in sys.stdin]  # saving input into table
    n_elements = int(input_matrix[0])  # number of elements
    m_elements = [int(m) for m in input_matrix[1].split()]  # masses of elements
    em_order = [int(em) for em in input_matrix[2].split()]  # order given
    em_order_copy = em_order.copy()
    dir_order = [int(d) for d in input_matrix[3].split()]  # order given by default
    dir_order_copy = dir_order.copy()
    cycle = []
    s_array = []  # array to store values of single cycle

    # dividing the whole cycle into smaller ones
    for i in range(n_elements):
        find(0, em_order, dir_order)
        cycle.append(s_array)
        s_array = []
        if em_order:
            for j in range(len(cycle[i])):
                em_order.remove(cycle[i][j])
                dir_order.remove(cycle[i][j])
        if em_order == []:
            break

    final_result = 0
    method1 = 0
    method2 = 0
    the_lightest_of_all = the_lightest(m_elements)  # mass of the lightest element

    for c in cycle:
        # a cycle with a single value
        if len(c) == 1:
            pass
        else:
            method1 = mass_s_cycle(c) + ((len(c) - 2) * mass_light_cycle(c))
            method2 = mass_s_cycle(c) + mass_light_cycle(c) + ((len(c) + 1) * the_lightest_of_all)
            if method1 <= method2:
                final_result += method1
            else:
                final_result += method2
    print(final_result)
