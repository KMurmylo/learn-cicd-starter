package auth

import (
	"errors"
	"net/http"
	"testing"
)

func TestAuth(t *testing.T) {
	header := http.Header{}
	_, err := GetAPIKey(header)
	if !errors.Is(err, ErrNoAuthHeaderIncluded) {
		t.Fatalf("Wrong error returned:%v", err)
	}
	header.Add("Authorization", "Bob")
	_, err = GetAPIKey(header)
	if err == nil {
		t.Fatalf("No error returned")
	}
	if err.Error() != "malformed authorization header" {
		t.Fatalf("Wrong error returned:%v", err)
	}
	header = http.Header{}
	header.Add("Authorization", "ApiKey")
	_, err = GetAPIKey(header)

	if err == nil {
		t.Fatalf("No error returned")
	}
	if err.Error() != "malformed authorization header" {
		t.Fatalf("Wrong error returned:%v", err)
	}
	header = http.Header{}
	header.Add("Authorization", "ApiKey SomeValue")
	output, err := GetAPIKey(header)
	if err != nil {
		t.Fatalf("Encountered error:%v", err)
	}
	if output != "SomeValue" {
		t.Fatalf("Incorrect result, got: %s expected: %s", output, "SomeValue")
	}

}
