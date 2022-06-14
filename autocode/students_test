package coverage

import (
	"fmt"
	"os"
	"strconv"
	"testing"
	"time"

	"github.com/stretchr/testify/assert"
	"github.com/stretchr/testify/require"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW
func TestLess(t *testing.T) {
	birthday1, _:= time.Parse("2006-Jan-02","1992-Jun-28")
	birthday2, _:= time.Parse("2006-Jan-02","2005-Oct-12")
	// birthday3, _:= time.Parse("2006-Jan-02","1997-Sep-10")
	people := People{
		Person{
			firstName: "Akzhol",
			lastName: "Kanybekuly",
			birthDay: birthday1,
		},
		Person{
			firstName: "Asylbek",
			lastName: "Kanybekuly",
			birthDay: birthday1,
		},
		Person{
			firstName: "Akzhol",
			lastName: "some",
			birthDay: birthday1,
		},
		Person{
			firstName: "some",
			lastName: "person",
			birthDay: birthday2,
		},
	}
	cases := []struct{
		name string
		i, j int
		expRes bool
	}{
		{
			name: "by firstname",
			i: 0,
			j: 1,
			expRes: true,
		},
		{
			name: "by lastname",
			i: 0,
			j: 2,
			expRes: true,
		},
		{
			name: "by birthday",
			i: 0,
			j: 3,
			expRes: false,
		},
	}

	assert.Equal(t, people.Len(), 4)

	for k,c:= range cases{
		t.Run(c.name, func(tr *testing.T) {
			assert.Equal(tr, people.Less(c.i, c.j), c.expRes, "case %d", k+1)
		})
	}

	people.Swap(0,1)
}

func TestMatrix(t *testing.T){
	cases := []struct{
		name string
		str string 
		expError error
		expRes *Matrix
	}{
		{
			name: "all ok",
			str: "1 2 3",
			expRes: &Matrix{rows:1, cols:3, data:[]int{1, 2, 3}},
		},
		{
			name: "not same length",
			str: "1 2 3\n1 2",
			expError: fmt.Errorf("Rows need to be the same length"),
		},
		{
			name: "not a number",
			str: "",
			expError: &strconv.NumError{Func:"Atoi", Num:"", Err:fmt.Errorf("invalid syntax")},
		},
	}

	for _,c := range cases {
		t.Run(c.name, func(tr *testing.T) {
			m,err := New(c.str)
			if c.expError != nil {
				assert.Nil(t, m)
				assert.NotNil(tr, err)
				assert.Equal(t, c.expError, err)
			} else {
				assert.Nil(tr, err)
			}
		})
	}
}

func TestRows(t *testing.T){
	str := "1 2 3"
	m,err := New(str)
	require.Nil(t, err)

	assert.Equal(t, m.Rows(), [][]int{{1,2,3}})
}

func TestCols(t *testing.T){
	str := "1 2 3"
	m,err := New(str)
	require.Nil(t, err)

	assert.Equal(t, m.Cols(), [][]int{{1},{2},{3}})
}

func TestSet(t *testing.T) {
	str := "1 2 3"
	m,err := New(str)
	require.Nil(t, err)

	assert.False(t, m.Set(1,0,5))
	assert.True(t, m.Set(0,0,5))
	assert.Equal(t, m, &Matrix{rows: 1, cols: 3, data: []int{5,2,3}})
}



